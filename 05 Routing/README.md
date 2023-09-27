
Show routing table
```
route -n -> depricated
```
```
ip route
ip r
```
you can user it for prohibit 
```
ip route add prohibit 1.1.1.1
```
reset
```
sudo ip route flush 1.1.1.1
```
Send Specific IP address from specific interface
```
sudo ip route add 1.1.1.1 via 172.31.96.1 dev eth0
```
you can show this route 
```
ip r
```

## Working with Static Routes
### Introduction
In this hands-on lab, you will need to create a script that modifies the routing table to prohibit connectivity to google.com. You'll also add an entry to use 10.0.1.20 as the gateway for the 10.0.8.0/24 subnet.

### Solution
Begin by logging in to the lab server using the credentials provided on the hands-on lab page:
```
ssh cloud_user@PUBLIC_IP_ADDRESS
 ```
Become the root user:
```
sudo su -
```
#### View the routing table, and prohibit connectivity to google.com.
You can view the routing table using the following command:
```
ip route show
```
You should install the `bind-utils` package which includes the host command, to get the IPs associated with google.com.
```
host google.com
```
Once you have the IP address(es), you can prohibit connectivity to them using the following command:
```
ip route add prohibit <IP_ADDRESS>
```
#### Add an entry for the 10.0.8.0/24 network to use 10.0.1.20 as the gateway
Add the following entry:
```
ip route add 10.0.8.0/24 via 10.0.1.20
```
#### Write a script that creates both entries
Using a text editor like vim, create and edit the file /home/cloud_user/routes.sh :
```
#!/bin/bash
   
ip route add prohibit <GOOGLE_IP>
ip route add 10.0.8.0/24 via 10.0.1.20
```
