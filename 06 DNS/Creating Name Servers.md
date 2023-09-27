# Creating Name Servers

## Introduction

We need to set up two DNS hosts, a master and a slave, as well as configuring a client to use our hosts.

> Note: This is not a secure implementation and should not be implemented in a production environment.
> 

We've been provided with three hosts:

**Server1**

This host (`dns1`) should be configured as a master DNS host for the *example.com* zone, with valid forward and reverse records.

**Server2**

This host (`dn2`) should be configured as a slave DNS host for `dns1`, and have an A record (and resolve) to *dns2.example.com*.

**Client1**

This host (`client`) should be configured to use *dns2.example.com* as it's primary DNS host, and successfully resolve *dns1.example.com* and *dns2.example.com* to their respective internal IPs.

## Get logged in

Use the credentials and server IP in the hands-on lab overview page to log into our lab server. Notice there are multiple machines we're working with. Pay attention in the lab guide, as the shell prompt will reveal which one we're working with at the moment.

## Install BIND on the Primary DNS Host

We're going to be running lots of things that require elevated privileges, so let's become `root` right off (`su -`), then we can get moving.

We need to install BIND prior to configuring it:

`[root@dns1]# yum install bind bind-utils`

Then we need to enable the service, but we won't start it until configuration is complete:

`[root@dns1]# systemctl enable named`

## Configure BIND on the Primary DNS Host

BIND's primary configuration file is `/etc/named.conf`. We need to edit that in order to configure BIND.

### Add the Local IP to the `listen-on` Line

Down in the `options` section, add our IP to the `listen-on port` line:

`listen-on port 53 { 127.0.0.1; 10.0.1.10;};`

### Limit Queries to `localhost` and the Secondary DNS host

We've got to add `dns2`'s IP to the `allow-query` line too, and add a new line that permit transfers to it:
```
allow-query     { localhost; 10.0.1.11; };
allow-transfer  { localhost; 10.0.1.11; };
```

### Disable Recursion

A few lines later, we want to disable recursion, changing `yese` to `no`:

`recursion no;`

### Add Zones

Just above the above the `includes` section, near the bottom of the file, we need to add forward and reverse zones:
```
zone "example.com" IN {
type master;
file "forward.example.com";
allow-update { none; };
};
zone "1.0.10.in-addr.arpa" IN {
type master;
file "reverse.example.com";
allow-update { none; };
};
```

We can save and exit the file now.

## Create Zone Files on the Primary DNS Host

Now we've got to create the zone files. We should locate them in `/var/named/`, and the names must match what we referenced in `/etc/named.conf`: `forward.example.com`, and `reverse.example.com`. Here are their contents:

### `forward.example.com`:

```$TTL 86400
@   IN  SOA     ns1.example.com. server1.example.com. (
        2018091201  ;Serial
        3600        ;Refresh
        1800        ;Retry
        604800      ;Expire
        86400       ;Minimum TTL
)
@           IN  NS  ns1.example.com.
@           IN  NS  ns2.example.com.
server1     IN  A   10.0.1.10
ns1         IN  A   10.0.1.10
server2     IN  A   10.0.1.11
ns2         IN  A   10.0.1.11
client1     IN  A   10.0.1.12
```
### `reverse.example.com`:

```$TTL 86400
@   IN  SOA     ns1.example.com. server1.example.com. (
        2018091201  ;Serial
        3600        ;Refresh
        1800        ;Retry
        604800      ;Expire
        86400       ;Minimum TTL
)
@           IN  NS  ns1.example.com.
@           IN  NS  ns2.example.com.
server1     IN  A   10.0.1.10
ns1         IN  A   10.0.1.10
server2     IN  A   10.0.1.11
ns2         IN  A   10.0.1.11
client1     IN  A   10.0.1.12
10          IN PTR server1.example.com.
10          IN PTR ns1.example.com.
11          IN PTR server2.example.com.
11          IN PTR ns2.example.com.
12          IN PTR client1.example.com.
```

## Verify the Configuration of the Primary DNS Host (10.0.1.10)

We'll check to see if everything is set up correctly:

`[root@dns1]# named-checkconf /etc/named.conf
[root@dns1]# named-checkzone example.com /var/named/forward.example.com
[root@dns1]# named-checkzone example.com /var/named/reverse.example.com`

## Start BIND on the Primary Host

Let's fire up BIND and see what happens:

`[root@dns1]# systemctl start named`

Then query our name server with `dig`:

`[root@dns1]# dig @localhost server1.example.com`

We've got to modify the firewall, so that the `dns2` host can query this one:
```
[root@dns1]# firewall-cmd --permanent --add-rich-rule='rule family="ipv4" source address="10.0.1.11" destination address=10.0.1.10 port port=53 protocol=tcp accept'
[root@dns1]# firewall-cmd --permanent --add-rich-rule='rule family="ipv4" source address="10.0.1.11" destination address=10.0.1.10 port port=53 protocol=udp accept'
[root@dns1]# firewall-cmd --reload
```
## Configure the Secondary Host

Over on `dns2`, we've got to install BIND and enable it. Just like on `dns1`, we're going to be running several things that require elevated privileges, so just become `root` right off (`su -`), and we'll get moving.

Install BIND and enable it:

`[root@dns2]# yum install bind bind-utils`

Then we've got to edit `/etc/named.conf`, like we did on `dns`.

### Add the Local IP to the `listen-on` Line

`listen-on port 53 { 127.0.0.1; 10.0.1.11;};`

### Limit Queries to the Local Subnet

`allow-query     { localhost; 10.0.1.0/24; };`

### Disable Recursion

`recursion no;`

### Add Zones

We've got to add the same zones we did on `dns1`. Again, this is down near the bottom of `named.conf`:

```zone "example.com" IN {
type slave;
file "/slaves/example.com.fwd";
masters { 10.0.1.10; };
};
zone "1.0.10.in-addr.arpa" IN {
type slave;
file "/slaves/example.com.rev";
masters { 10.0.1.10; };
};
```

## Start BIND on the Secondary Host

Verify the configuration:

`[root@dns2]# named-checkconf /etc/named.conf`

Now we can enable the service and start it:

`[root@dns2]# systemctl enable named
[root@dns2]# systemctl start named`

We can verify whether our configuration is good:

`[root@dns2]# dig @localhost server1.example.com`

Now we'll enable DNS traffic through the firewall:

`[root@dns2]# firewall-cmd --permanent --add-service=dns && firewall-cmd --reload`

Phew, the servers are done. Now we can move on to the client.

## Configure the Client to Use the Secondary DNS Host (10.0.1.11) for DNS

Like we did on the servers, become `root` right off (`su -`) and then we can proceed.

First, we'll install NetworkManager and start it:
```
[root@client]# yum -y install NetworkManager
[root@client]# systemctl enable NetworkManager && systemctl start NetworkManager
```
Installing the `bash-completion` package will be handy too:

`[root@client] yum -y install bash-completion`

Then, we'll configure the interface to be static, assign the secondary host IP as the DNS, and the DNS searches be on `example.com`:
```
[root@client]# nmcli con mod System\ ens5 ipv4.method manual ipv4.addresses 10.0.1.12/24 ipv4.gateway 10.0.1.1 ipv4.dns
10.0.1.11 ipv4.dns-search example.com
```
We've got to remove the `ec2.internal` search domain from `/etc/resolv.conf`:

`[root@client]# sed -i '/ec2.internal/d' /etc/resolv.conf`

Restart networking to pickup the configuration change:

`[root@client]# systemctl restart network`

Now we can verify that it works, with `dig`:

`[root@client]# dig server1.example.com`
