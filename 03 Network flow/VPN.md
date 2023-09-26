## VPN :: USE CASES
A VPN connection is an extension of a private network, using the IP connectivity of the internet to connect remote clients to
remote sites in an encrypted private connection.

- Secure private network traffic over an insecure public network
- Permit connections to an internal corporate resource from a remote location
- Connect two separated private networks together
- The routing table lists `destinations` and `gateways` for the networks a host belongs to

## VPN :: SITE-TO-SITE
![image](https://github.com/h0x3ein/network-by-doing/assets/75008854/f1cd7faf-2a34-4c21-86c1-4b9e87ed226a)

A site-to-site VPN connects two parts of a private network (or two private networks). This allows an organization to have
routed connections between separate offices, or with other organizations, over the Internet. A routed VPN connection
across the Internet logically operates as a dedicated Wide Area Network (WAN) link.
## VPN :: REMOTE ACCESS VPN
![image](https://github.com/h0x3ein/network-by-doing/assets/75008854/8923aecb-e809-4dd1-a407-f97629a0e263)

A remote access VPN connection is made by a remote access client. A remote access client is a single computer connecting
to a private network from a remote location. The VPN server provides access to the network resources where the VPN server
is connected. The packets sent across the VPN connection originate at the VPN client.

## VPN :: THE TUNNEL
Tunneling permits the encapsulation of one type of protocol packing within the datagram of a different protocol, for
instance, sending TCP/IP traffic over the internet.

For PPTP and Layer Two Tunneling Protocol (L2TP), a tunnel is similar to a session. Each end of the tunnel must agree to the
tunnel connection, and will negotiate configuration variables such as address assignment, encryption, and compression
parameters. The mechanism used to create, maintain and end the tunnel is the tunnel management protocol.

Only after the tunnel is established can data be sent. When the tunnel client sends network data to the tunnel server, the
tunnel client appends a tunnel data transfer protocol header to the payload. The client then sends the encapsulated (and
usually encrypted) data to the tunnel server. The tunnel server accepts the data, removes the tunnel data, and forwards the
payload to the destination network within the VPN.

## VPN:: CONCLUSION
- [ ] A VPN can be used to securely connect a client to a `private network`
- [ ] A VPN can be used to securely connect `two private networks`
- [ ] A VPN works by `encapsulating` and `encrypting` the network data at the client end, and decrypting at the destination end
- [ ] `There’s a lot more to VPNs than has been covered`
