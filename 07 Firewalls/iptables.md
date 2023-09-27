

## IPTABLES :: RULES
![image](https://github.com/h0x3ein/network-by-doing/assets/75008854/aacfcc38-1da9-42de-a79c-6bac1a092caf)


## IPTABLES :: STATES
- **NEW** A new packet not associated with any existing connection
- **ESTABLISHED** Established traffic (SYN/ACK)
- **RELATED** Packets associated with a connection already in the system, but not an existing connection
- **INVALID** Unrouteable or unidentifiable packets not associated with an existing connection or suitable for a new connection
- **UNTRACKED** Packets set in the raw table chain to bypass connection tracking
- **SNAT** Source modified by NAT
- **DNAT** Destination modified by NAT
