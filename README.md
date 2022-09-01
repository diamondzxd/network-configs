# network-configs

## For Hetzner
### Interfaces

```bash
### Hetzner Online GmbH installimage

source /etc/network/interfaces.d/*

auto lo
iface lo inet loopback
iface lo inet6 loopback

auto enp0s31f6
iface enp0s31f6 inet static
  address 88.99.139.8
  netmask 255.255.255.192
  gateway 88.99.139.1
  # route 88.99.139.0/26 via 88.99.139.1
  up route add -net 88.99.139.0 netmask 255.255.255.192 gw 88.99.139.1 dev enp0s31f6

iface enp0s31f6 inet6 static
  address 2a01:4f8:10a:2347::2
  netmask 128
  gateway fe80::1

# IPv4 config for a sample /28 Subnet. 3 IPs will not be usable due to network, gateway and broadcast addresses
auto vmbr0
iface vmbr0 inet static
        address  178.63.220.177
        netmask  29
        bridge-ports none
        bridge-stp off
        bridge-fd 0
        bridge_maxwait 0
        pre-up brctl addbr vmbr0
        # Add all your usable IPv4's like this
        up ip route add 178.63.220.178/32 dev vmbr0
        up ip route add 178.63.220.179/32 dev vmbr0
        up ip route add 178.63.220.180/32 dev vmbr0
        up ip route add 178.63.220.181/32 dev vmbr0
        up ip route add 178.63.220.182/32 dev vmbr0
        up ip route add 178.63.220.183/32 dev vmbr0
        up ip route add 178.63.220.184/32 dev vmbr0
        up ip route add 178.63.220.185/32 dev vmbr0
        up ip route add 178.63.220.186/32 dev vmbr0
        up ip route add 178.63.220.187/32 dev vmbr0
        up ip route add 178.63.220.188/32 dev vmbr0
        up ip route add 178.63.220.189/32 dev vmbr0
        up ip route add 178.63.220.190/32 dev vmbr0
        
iface vmbr0 inet6 static
        address  2a01:4f8:10a:2347::3
        netmask  64

#Internal Bridge for host and VM communication.
auto vmbr1
iface vmbr1 inet static
	address 192.168.1.1
	netmask 24
	bridge-ports none
	bridge-stp off
        bridge-fd 0
        bridge_maxwait 0

#Empty bridge for pfSense or an internal virtualized router
auto vmbr2
iface vmbr2 inet static
        bridge-ports none
        bridge-stp off
        bridge-fd 0


```

### sysctl.conf

```conf
### Hetzner Online GmbH installimage
# sysctl config
net.ipv4.ip_forward=1
net.ipv6.conf.all.forwarding=1
net.ipv4.conf.all.rp_filter=1
net.ipv4.icmp_echo_ignore_broadcasts=1
# ipv6 settings (no autoconfiguration)
net.ipv6.conf.default.autoconf=0
net.ipv6.conf.default.accept_dad=0
net.ipv6.conf.default.accept_ra=0
net.ipv6.conf.default.accept_ra_defrtr=0
net.ipv6.conf.default.accept_ra_rtr_pref=0
net.ipv6.conf.default.accept_ra_pinfo=0
net.ipv6.conf.default.accept_source_route=0
net.ipv6.conf.default.accept_redirects=0
net.ipv6.conf.all.autoconf=0
net.ipv6.conf.all.accept_dad=0
net.ipv6.conf.all.accept_ra=0
net.ipv6.conf.all.accept_ra_defrtr=0
net.ipv6.conf.all.accept_ra_rtr_pref=0
net.ipv6.conf.all.accept_ra_pinfo=0
net.ipv6.conf.all.accept_source_route=0
net.ipv6.conf.all.accept_redirects=0

```
