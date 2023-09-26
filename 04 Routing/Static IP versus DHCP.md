## STATIC VERSUS DHCP :: DIFFERENCES
|Static|Dynamic|
| --- | --- |
|Dedicated, unchanging IP address assigned to the device|Dynamic address assigned from a pool of IP addresses within the DHCP scope|
|Upon setting it, you must also specify the subnet, gateway, and DNS host information|DHCP will normally provide subnet, gateway, and DNS information upon assigning an IP address|
|Not dependent on DHCP for anything|Dependent on DHCP upon lease expiration|
|Typically used for important network devices and hosts that require absolute connectivity|Typically used for hosts and clients requiring transient connections*|
||DHCP is used for managing the IP addresses of a large number of hosts|

## STATIC VERSUS DHCP :: CONSIDERATIONS
- Using DHCP creates three potential points of failure in network connectivity: the DHCP host itself, a rogue DHCP host, and DNS
- The DHCP host becomes an issue if it is misconfigured - especially if you are dependent upon reservations for static-like IP assignment.
- The potential exists for a rogue DHCP host to present network configurations that could route traffic to a different router for nefarious purposes.
- If host IPs are changing, you’ll need to rely on FQDNs for host to host communication, placing a dependency on DNS for FQDN to IP resolution.

- DHCP makes managing thousands of host IPs in a virtual or automated infrastructure on a secure network much easier.

  ## STATIC VERSUS DHCP :: DHCP LEASES
- The DHCP server will grant a lease on an IP address – assigning it to the host for a period of time
- The DHCP request and offer are layer 2 broadcasts (similar to ARP requests) and requires a running DHCP client
- The DHCP server uses UDP port 67, and the Client uses UDP port 68
- You can use reservations to make sure the same host gets a new lease on the same IP upon expiration

View lease information on the host:
```
$ cat /var/lib/dhclient/dhclient.leases
```
Lookup DHCP host:
```
$ sudo grep "DHCPOFFER" /var/log/messages
```
## STATIC VERSUS DHCP :: DHCP SEQUENCE
![image](https://github.com/h0x3ein/network-by-doing/assets/75008854/86cfd2d8-28cd-40b5-a626-739fc5d58dd0)

## STATIC VERSUS DHCP :: STATIC IP
You will need to provide the following information to set a static IP:
- IP Address
- The netmask
- The gateway IP
- The DNS host (optional)
- The DNS domain (optional)

## STATIC VERSUS DHCP :: CONCLUSION
A `DHCP host` provisions IP addresses to network devices upon request
CLI example of lease information
The DHCP request is a Layer 2 broadcast, the sequence is `Discover, Offer, Request, Acknowledge`
Wireshark example of the `DHCP request` sequence
To use a `static IP`, you must provide the network information
`CLI example` of going from DHCP to static, and back to DHCP
