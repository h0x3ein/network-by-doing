## ROUTING :: THE BASICS 
- A router is a layer 3 device, functioning at the IP level
- A router forwards data packets between networks
- The routing table is a static table mapping of the best path to a network destination
- The routing table lists destinations and gateways for the networks the host belongs to

![image](https://github.com/h0x3ein/network-by-doing/assets/75008854/6ca489f7-3ec3-4bf1-a1fa-bcbca602fcbe)

- If the destination is outside of the local network, use the gateway
- If the destination is inside the local network (172.31.69.0/20), don’t use the gateway

### ROUTING :: STATIC ROUTES
- Static routes are `manually` configured routes
- Static routes are for traffic that must not (or should not) go through the default gateway

  ![image](https://github.com/h0x3ein/network-by-doing/assets/75008854/e5460436-4504-4a89-9c2b-bde97bf07d61)

- Example: `172.31.96.0/20` is the server network, and the office network is `10.0.0.0/8`
- The office network is accessible via a router with the IP of `172.31.96.2` on the server network
- A route would need to be added to permit this host to communicate with the office network using that router
### ROUTING :: BGP
- Border Gateway Protocol
- Routing protocol used to route traffic across the internet – it’s how the internet works


BGP is a Layer 4 protocol sitting on top of TCP - this makes it simpler than OSFP, as it doesn’t manage what TCP handles
There is no discovery; peers that have been manually configured to exchange routing information form a TCP connection
Organizations can use BGP for true multi-homing their corporate network

An `ASN` (Autonomous System Number) is required to implement BGP peering
This is a special number assigned by `IANA` for use primarily with BGP that identifies each network on the internet
Two routers that have established a connection and exchanged BGP information are `BGP peers`, exchanging routing
information between them via BGP sessions over TCP

### ROUTING :: CONCLUSION
- [ ] Routers connect `different networks`
- [ ] Routing information is contained in a `routing table`
- [ ] `Static routes` can be used for connections that can’t (or shouldn’t) use the default gateway
- [ ] `BGP` is the routing protocol that enables the internet to work
