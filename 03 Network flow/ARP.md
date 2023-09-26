## ARP :: DEFINITION
Address Resolution Protocol.
ARP is a communication protocol used for discovering the MAC address associated with a given network layer address (IP address).
Put simply, ARP is used for mapping an IP address to a MAC address on the network.

## ARP :: SEQUENCE
![image](https://github.com/h0x3ein/network-by-doing/assets/75008854/64317b73-8ee7-4528-95a7-359726418383)

## ARP :: IN ACTION
![image](https://github.com/h0x3ein/network-by-doing/assets/75008854/6597e759-5283-4dd7-aafe-c08714fc0751)

## ARP :: CONCLUSION
- [ ] ARP is necessary to map `Layer 3` (IP) addressing to `Layer 2` (MAC) addressing
- [ ] This is used for `local area network` connections
- [ ] Connections outside of the local area network, go through the `gateway` (ARP request for gateway IP)
- [ ] The `ARP table` is dynamically updated, and can be viewed using the `ip n` command.
