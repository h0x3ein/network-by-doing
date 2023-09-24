# Important Information

- [ ] **MAC Address**: Unique fingerprint of the network interface
- [ ] **IP Address**: Unique address on the network
- [ ] **Subnet**: Separates the IP into network and host addresses
- [ ] **Gateway**: The connection leading outside of the local network
- [ ] **DNS Host**: Translates hostnames into IP addresses
- [ ] **DNS Domain**: The lookup domain for the host

## ifconfig
### lo interface:
Is a special virtual interface that the host uses to communicate to `itself`
```
eth0: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        inet 172.18.0.1  netmask 255.255.0.0  broadcast 172.18.255.255
        ether 02:42:ed:4e:de:43  txqueuelen 0  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 235972  bytes 241369067 (241.3 MB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 235972  bytes 241369067 (241.3 MB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

## ip adddr show
```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: wlp0s20f3: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN group default qlen 1000
    link/ether 0c:9a:3c:9a:2e:b4 brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.9/24 brd 192.168.1.255 scope global dynamic noprefixroute wlp0s20f3
       valid_lft 86197sec preferred_lft 86197sec
    inet6 fe80::9b08:6296:368e:af3f/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
```
## nmcli
```
wlp0s20f3: connected to TP-Link_3E06
        "Intel Wi-Fi"
        wifi (iwlwifi), 0C:9A:3C:9A:2E:B4, hw, mtu 1500
        ip4 default
        inet4 192.168.1.9/24
        route4 0.0.0.0/0
        route4 169.254.0.0/16
        route4 192.168.1.0/24
        inet6 fe80::9b08:6296:368e:af3f/64
        route6 fe80::/64

lo: unmanaged
        "lo"
        loopback (unknown), 00:00:00:00:00:00, sw, mtu 65536

DNS configuration:
        servers: 192.168.1.1
        domains: domain.name
        interface: wlp0s20f3

Use "nmcli device show" to get complete information about known devices and
"nmcli connection show" to get an overview on active connection profiles.

```
### nmcli d show
```
GENERAL.DEVICE:                         wlp0s20f3
GENERAL.TYPE:                           wifi
GENERAL.HWADDR:                         0C:9A:3C:9A:2E:B4
GENERAL.MTU:                            1500
GENERAL.STATE:                          100 (connected)
GENERAL.CONNECTION:                     TP-Link_3E06
GENERAL.CON-PATH:                       /org/freedesktop/NetworkManager/ActiveConnection/24
IP4.ADDRESS[1]:                         192.168.1.9/24
IP4.GATEWAY:                            192.168.1.1
IP4.ROUTE[1]:                           dst = 0.0.0.0/0, nh = 192.168.1.1, mt = 20600
IP4.ROUTE[2]:                           dst = 169.254.0.0/16, nh = 0.0.0.0, mt = 1000
IP4.ROUTE[3]:                           dst = 192.168.1.0/24, nh = 0.0.0.0, mt = 600
IP4.DNS[1]:                             192.168.1.1
IP4.DOMAIN[1]:                          domain.name
IP6.ADDRESS[1]:                         fe80::9b08:6296:368e:af3f/64
IP6.GATEWAY:                            --
IP6.ROUTE[1]:                           dst = fe80::/64, nh = ::, mt = 600
.
.
.
.
.
.
.
.
```
## ip route show
```
default via 192.168.1.1 dev wlp0s20f3 proto dhcp metric 600 linkdown 
192.168.1.0/24 dev wlp0s20f3 proto kernel scope link src 192.168.1.9 metric 600 linkdown
```

## routel
```
         target            gateway          source    proto    scope    dev tbl
        default        192.168.1.1                     dhcp         wlp0s20f3 
   169.254.0.0/ 16                                              linkwlp0s20f3 
    172.17.0.0/ 16                      172.17.0.1   kernel     linkdocker0 
    172.18.0.0/ 16                      172.18.0.1   kernel     linkbr-84cae0ead9c0 
   192.168.1.0/ 24                     192.168.1.9   kernel     linkwlp0s20f3 
     127.0.0.0/ 8            local       127.0.0.1   kernel     host     lo local
      127.0.0.1              local       127.0.0.1   kernel     host     lo local
127.255.255.255          broadcast       127.0.0.1   kernel     link     lo local
     172.17.0.1              local      172.17.0.1   kernel     hostdocker0 local
 172.17.255.255          broadcast      172.17.0.1   kernel     linkdocker0 local
     172.18.0.1              local      172.18.0.1   kernel     hostbr-84cae0ead9c0 local
 172.18.255.255          broadcast      172.18.0.1   kernel     linkbr-84cae0ead9c0 local
    192.168.1.9              local     192.168.1.9   kernel     hostwlp0s20f3 local
  192.168.1.255          broadcast     192.168.1.9   kernel     linkwlp0s20f3 local
            ::1                                      kernel              lo 
        fe80::/ 64                                   kernel         wlp0s20f3 
            ::1              local                   kernel              lo local
fe80::9b08:6296:368e:af3f              local                   kernel         wlp0s20f3 local

```

# Locating the Network Information (Task)
Being able to locate the IP address, netmask, gateway, DNS nameserver, and domain is critical to understanding Linux networking. In this Learning Activity, you will populate a text file with this information.
## find `IP Address` and `Netmask` and `Gateway` and `DNS Domain`
### tip
You can use `nmcli` or `nmcli d show <NETWORK NAME>` for find information
