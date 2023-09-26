## DNS :: DEFINITION
- Domain Name Service
- DNS is a `Layer 7` communication protocol used for discovering the IP address associated with a given domain name.
- Put simply, DNS is used for mapping a domain name to an IP address on the network.

## DNS :: QUERY
An `FQDN` (fully qualified domain name) is the complete domain name for a specific host on the network.
When a computer wants to initiate a connection to an FQDN, such as `www.example.com`, it needs to
know where the host is on the network.
The computer will send a query to the DNS server, asking it to resolve the FQDN to an IP address, and
then looks at the routing table to determine where to send the request.

## DNS :: HOW IT WORKS
#### step1
Using `www.example.com`, there is an implied period after `.com`
The query is going to start at the far right, with the period after the `.com`
This query is resolved by the root servers, and then forwarded to the TLD servers

#### step2
The TLD (Top Level Domain) servers resolve the `.com`
Root Servers are available to answer domain queries regarding TLDs such as `.com`
The query is then forwarded to the name servers for the domain, in this case `example.com`

#### step3
The name servers resolve the domain portion of the query, `example.com`
The name servers may also be able to resolve the `www` portion
Or they may need to forward the query to additional authoritative DNS hosts managing the zones within
the domain.

## DNS :: RESOLUTION
![image](https://github.com/h0x3ein/network-by-doing/assets/75008854/2c12fcd5-dfa9-4240-885a-c5cd6a219b64)

## DNS :: CONCLUSION
- [ ] DNS is necessary to map `FQDN` addresses to `Layer 3`(IP) addresses
- [ ] This is used for `internal` and `external` connections
- [ ] Resolution begins with the `TLD`, and progresses to the name server for the domain
- [ ] Once the domain name has been `resolved` to an IP, the connection can begin
