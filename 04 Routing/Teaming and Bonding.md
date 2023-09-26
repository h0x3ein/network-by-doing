## TEAMING AND BONDING :: USE CASE

![image](https://github.com/h0x3ein/network-by-doing/assets/75008854/e4179c4b-8071-4933-b9fc-e910b13b20e4)

Redundant connections
We can use a network Team or Bond to achieve this
Teaming and Bonding are similar, but there are differences

## TEAMING AND BONDING :: ADVANTAGES
### Teaming
- Support for IPv6 link monitoring
- Able to work with D-Bus and Unix Domain Sockets
- Load balancing for LACP support
- Leverages NetworkManager and associated tools

### Bonding
Doesn’t require teamd?
Works in a virtual environment

## TEAMING AND BONDING :: DEFAULT BEHAVIOUR
### Teaming
- Starting the master (team0) interface will not automatically start the port interfaces (slave1).
- Starting a port interface (slave1) will start the master interface (team0).
- Stopping the master interface (team0) also stops the port interfaces (slave1, slave2, etc).
- A master without ports will start static IP connections.
- A master without ports waits for ports when starting DHCP connections.
- A master with a DHCP connection waiting for ports completes when a port with a carrier is added.
- A master with a DHCP connection waiting for ports continues waiting when a port without a carrier is added.

## TEAMING AND BONDING :: TEAM RUNNERS
### Teaming
- **broadcast**: Transmit data over all ports
- **round-robin**: Transmit data over all ports in sequence
- **active-backup**: One port is used while the other is reserved as a backup
- **loadbalance**: Active load balancing and port selection
- **lacp**: Implements the 802.3ad Link Aggregation Control Protocol

## TEAMING AND BONDING :: LINK WATCHERS
### Teaming
- ethtool: Default, watches for link state changes
- arp_ping: Monitors availability of MAC addresses using ARP
- nsna_ping: Neighborhood advertisement and neighborhood solicitation from the IPv6 neighbor
- discovery are used to monitor neighbor’s interface

`Only *ethtool* should be used when using LACP`

## TEAMING AND BONDING :: CONCLUSION
- Teaming and Bonding are similar, but Teaming has some advantages
- Example: Bonding multiple NICs
- Example: Teaming Multiple NICs
- There is some nuance to Teaming behavior that should be understood
