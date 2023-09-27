# Setting a Static IP

## The Scenario

A business unit is complaining that their job server is unable to connect to `acloudguru.com`. This is breaking integrations for multiple reporting applications.

## Get logged in

Use the credentials and server IP in the hands-on lab overview page to log into our lab server. Once we're in, we can get moving.

## Verify the Issue and Check `/etc/nsswitch.conf`

Switch to root user:

`sudo -i`

We'll first need to verify that the issue exists by attempting the `curl` the header of `acloudguru.com`:

`curl -I https://acloudguru.com/`

Next, we'll have to verify that nothing is missing in `nsswitch.conf`, and we should pay attention to the ordering of the `hosts` value. If we edit `/etc/nsswitch.conf`, we'll see that something is missing:

`hosts:      files myhostname`

That line should go like this:

`hosts:      files dns myhostname`

## Verify `/etc/hosts` Contents

We'll want to make sure there aren't any entries in this file that would cause issues:

`cat /etc/hosts`

In there, we see a line

`127.0.0.1   acloudguru.com`

The server we're logged into is *probably* not supposed to be *acloudguru.com*, so let's erase that line and save the file.

If we run our `curl` command again, our terminal hangs. Something is still wrong. Kill the curl with `Ctrl + C` and let's see what else might fix the problem.

## Determine If the DNS Host is Listening on TCP Port 53

Where is our `/etc/resolv.conf` pointing?

`cat /etc/resolv.conf`

Let's see if the nameserver listed in there is listening on TCP port 53. We'll know by running this:

`telnet 10.0.1.1 53`

We're getting no response.

## Check Resolution Using the 10.0.0.2 DNS Host

There's another possible DNS server kicking around, on 10.0.0.2. Now that we've verified that the host listed in `/etc/resolv.conf` isn't available on TCP port 53, check if resolution is working on the DNS host `10.0.0.2`:

`dig @10.0.0.2 acloudguru.com`

Hey, we're getting a response. This one looks good.

## Change the Configuration to Use the 10.0.0.2 Host

We can do this with network manager, or by editing `/etc/resolv.conf`. If we restart networking, this is the IP that will be used via DHCP. Let's go the network manager route and then restart the network. Afterward, we'll see what `resolv.conf` looks like, and try the dig command again:
```
nmcli con mod System\ ens5 ipv4.dns "10.0.0.2"
service NetworkManager restart
cat /etc/resolv.conf
dig acloudguru.com
curl -I https://acloudguru.com/
```
The new nameserver should be in `resolv.conf`, and the `dig` command should have printed a bunch of domain server related information.
