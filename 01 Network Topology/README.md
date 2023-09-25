## Switch
Is a network device used for local area network.
```
Switches forward packets within the internal network
```
## Router
```
Routers forwards packets between networks
```

Data travels through both to reach a destination outside of the LAN

# OSI Layer
|Layers|Description|
| --- | --- |
|Application|the interface permitting the user to send and receive data through clients and applications|
|Presentation|converts the request from the application into a universal format|
|Session|permits the ability to open, close, and manage a session between the process and response|
|Transport|efines how data will be sent, providing **validation** and security|
|Network|looks for the best path to reach the destination [ IP ]|
|Data Link|handles communication between adjacent nodes [ MAC ]|
|Physical|handles bit level transmission between network nodes|

### Application
**Conseptual** -> `The phone` is the interface used by the user to place the order.

**actual** -> a user clicking on a link within a web browser. The browser application provides the interface for the user to interact with the content provided by the remote web server

### Presentation
**conceptual** the individual using the telephone needs to be speaking a language the person on the other end can understand.

**actual** the web browser renders the page by converting the files stored on the remote server into formats that permit displaying the content. In the case of the web browser, this includes image formats such as jpeg and gif being converted into actual images on the screen.

### Session
**conceptual** when our user dialed the telephone to place the order, someone on the other end needed to pick up so the conversation could begin.

**actual** when a user clicks a link in a web browser, the browser will initiate a TCP connection to the web web server. The web server will send a response and close the connection. The browser will manage the additional TCP connections necessary to load assets externally referenced by the web server.

### Session
**conceptual** our user has placed the order and is waiting on delivery. Quality control has mechanisms in place to ensure the user is sent what the requested, and nothing else.
**actual** the web browser breaks up the TCP requests into manageable portions, applies a label to protect the ordering, and transports the pieces across the sessions.

### Network
**conceptual** the order has been fulfilled and shipped. The shipping provider uses GPS to determine the most direct and efficient route to deliver the package.

**actual** the web browser computer uses the IP address to determine if the web page is `local` or `remote`, and how to reach the remote IP via the `default gateway`. The computer creates a message (packet) and addresses it to the web server with it’s own return address.

### Data Link
**conceptual** the shipping company needs to know the full delivery address to successfully deliver the order. 

**actual** the packets are structured into messages call frames, to be sent to the default gateway. These frames contain the source and destination IP addresses, as well as the source and local destination MAC addresses.

### Phisical
**conceptual** the shipping company’s truck navigates a network of roads and interstates to deliver the order to the delivery address.

**actual** this layer is hardware specific, and is the actual physical connection between the computer and the network. The raw bits are transmitted as pulses of electricity (or light) over the network medium.

## OSI :: EXAMPLE PROTOCOLS
|Layers|Protocols|
| --- | --- |
|Application|**HTTP** - POP3 - DNS - SOAP|
|Presentation|TLS - **SSL** - MIME - JPEG - GIF|
|Session|LDAP - NetBios - PPTP - RPC - SMB - **SSL**|
|Transport|**TCP** - UDP - SPX - iSCSI|
|Network|**IP** - IPSec - ICMP - RIP|
|Data Link|**Ethernet** - Frame Relay - IEEE 802.11 (WiFi) -  PPP - VLAN - MAC|
|Physical|**Ethernet physical** - IEEE 1394 (firewire) - Infrared|

## OSI :: TROUBLESHOOTING
|Layers|Troubleshooting|
| --- | --- |
|Application|Verify application function and DNS|
|Presentation|Rarely issues at this layer if application is performing normally|
|Session|Rarely issues at this layer if application is performing normally|
|Transport|Verify blocked (or damaged) ports, firewalls, and QoS|
|Network|Verify addressing and routing configuration, bandwidth, and authentication|
|Data Link|Verify switch and VLAN configurations as well as MAC addressing and IP conflicts|
|Physical|Verify physical components|


# IP Address Anatomy
It is the address of your device on its network -> like house number on a street


<img src="https://github.com/h0x3ein/network-by-doing/assets/75008854/d2a4d887-4bf6-498f-b6a1-2af27b92b6df" width="600" height="300">

## IP ANATOMY :: IPv4 CLASSES

![2023-09-25_18-28](https://github.com/h0x3ein/network-by-doing/assets/75008854/990630e5-ee93-4550-a6cb-3d80daf1c9ad )

## CLASSES AND SUBNETS

![2023-09-25_18-29](https://github.com/h0x3ein/network-by-doing/assets/75008854/ab7bcb33-6ffb-4077-a44d-47b2af03bb28)

## IP ANATOMY :: PRIVATE NETWORKS
![2023-09-25_18-29_1](https://github.com/h0x3ein/network-by-doing/assets/75008854/b2bf4e37-b099-4dd6-ac1c-fbb5e0f220a8)

## IP ANATOMY :: NETMASKS AND SUBNETS

![2023-09-25_18-30](https://github.com/h0x3ein/network-by-doing/assets/75008854/c3549a34-0c6a-4173-90f0-b82136526993)

## IP ANATOMY :: CIDR
![2023-09-25_18-31](https://github.com/h0x3ein/network-by-doing/assets/75008854/3fbe997d-cf25-44eb-b7c5-a6d2c54ebb97)

## IP ANATOMY :: Network Address Translation
Network address translation (`NAT`) is a method of remapping one IP address space into another by modifying network address information in the IP header of packets while they are in transit across a traffic routing device.

![2023-09-25_18-32](https://github.com/h0x3ein/network-by-doing/assets/75008854/8f0e34e4-8e3d-4627-afdc-87cc7c25362d)


## IP ANATOMY :: CONCLUSION
- [ ]  IP addresses are necessary for `Layer 3` addressing on the network
- [ ]  An `IPv4` address is a `32bit` number separated into 4 8bit octets by periods
- [ ]  An `IPv6` address is a `128bit` number separated into 8 16bit sections by a colons
- [ ]  A `subnet` is a subsection of the network, and determines the IP range and size
- [ ]  A `classful` network uses a portion of the IP address as the network address
- [ ]  `CIDR` permits more flexibility in network size over the traditional classful design


