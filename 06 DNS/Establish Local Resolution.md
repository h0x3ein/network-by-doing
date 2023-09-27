# Establish Local Resolution

## Introduction

In this hands-on lab, you are tasked with establishing local resolution for a domain name, to permit localized application testing.

## Solution

1. Begin by logging in to the lab server using the credentials provided on the hands-on lab page:
    
    `ssh cloud_user@PUBLIC_IP_ADDRESS`
    
2. Become the `root` user:
    
    `sudo su -`
    

### Verify the Contents and Order of `/etc/nsswitch.conf`

1. You'll want to verify that `files` comes before `dns` in the `hosts` section of `/etc/nsswitch.conf`.
    
    `vim /etc/nsswitch.conf`
    
    The `hosts` line should look like this:
    
    `hosts:	files dns myhostname`
    

### Modify `/etc/hosts` to Include *[www.example.com](http://www.example.com/)*

1. You will need to modify `/etc/hosts` to resolve `www.example.com` to your local IP. Use your local IP: `10.0.1.10`.
    
    `vim /etc/hosts`
    
    Add the following line:
    
    `10.0.1.10	www.example.com`
    

### Verify That You Can Now Connect to the Locally Running Webserver at *[www.example.com](http://www.example.com/)*

1. You should get the same output if you `curl` either `localhost` or `www.example.com`.

`curl localhost`

`curl www.example.com`
