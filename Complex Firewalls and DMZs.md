# Complex Firewalls and DMZs

This lesson will expand on knowledge of firewalls and introduce the idea of a DMZ

## Topics covered

At the end of this lesson, you will know:
- What a DMZ is
- How to build a network using DMZs and firewalls
- How to configure firewalls to create a DMZ


## What is a DMZ?
DMZ stands for demilitarised zone

DMZs are useful for protecting "networks"/hosts from malicious threats but still allowing a limited access to and from the interent. DMZs have a different level of security than the remainder of a "network". 

## How Do DMZs Work?
DMZs refers to segments of a network created between an external network like the internet and an internal network such as an internal LAN. Normally, the DMZ is isolated from the external network, the Internet, and the internal network by a firewall. By installing a server that is open to the public, such as a web server, in the DMZ, even if there is unauthorized access from the outside, the network is isolated, and therefore, a security effect can be expected. This will provide a security effect even if there is unauthorized access from the outside

For example in the previous lesson our network had a security level of 100 but a DMZ may have a security level of 50. When we assign security levels, we assign them to interfaces, not networks. However, in this lesson there will still be references to assigning security levels to networks for simplicity's sake. 




### Recommended Knowledge 
-[Firewall Intro]()


### Third party resources

* [What is a Firewall?](https://www.youtube.com/watch?v=hfyLjRZmEFc)


## Instructions

Download the project from here: 

### 1. Create the following network
![](https://github.com/mooroon/NetworkingA13/blob/main/IMAGES/Screen%20Shot%202024-05-08%20at%208.41.11%20pm.png)

You should include
- 3 PCs
- 1 Server
- 1 Switch

### 2. Configure IP addresses 
Configure the PCs and server with IPv4 address and Subnet Mask according to the IPs given:

Server = 10.13.10.1	255.0.0.0

PC0 =	10.13.10.2	255.0.0.0

PC1	= 10.13.10.3	255.0.0.0

PC2	= 10.13.10.4	255.0.0.0

We can do this by going to Desktop on each PC/Server and using IP Configuration, ensuring it is set as static and then typing the IP address and subnet mask into their respective fields.
We can also assign IP addresses using the command terminal of the PCs, we can use this command:

```cmd

C:\>ipconfig 1.13.10.2 255.0.0.0

```

![](https://github.com/mooroon/NetworkingA13/blob/main/IMAGES/Screenshot%20from%202024-05-08%2009-37-57.png)
![](https://github.com/mooroon/NetworkingA13/blob/main/IMAGES/Screenshot%20from%202024-05-08%2009-38-03.png)

### 3. Configuring The Firewall
Now that we have assigned IP addresses we can configure the firewall
- Select the server
- Go to desktop
- Click on firewall IPv4
- Turn on Services
- Deny the ICMP protocol and set the remote IP to 0.0.0.0 and the remote wildcard mask to 255.255.255.255
- Click Add

![](https://github.com/mooroon/NetworkingA13/blob/main/IMAGES/Screenshot%20from%202024-05-08%2009-39-48.png)

- Next, allow the IP protocol and set the remote IP to 0.0.0.0 and the remote wildcard mask to 255.255.255.255 (the same as the ICMP)
- Click Add

![](https://github.com/mooroon/NetworkingA13/blob/main/IMAGES/Screenshot%20from%202024-05-08%2009-40-48.png)

### 4. Test ICMP protocol 
We can test what we have just configured by pinging the Server from a PC
- Click any PC
- Go to desktop and then command prompt
- Ping the server by using the command:
```cmd
C:\>ping 10.13.10.1 255.0.0.0
```
As shown by the image, all requests should time out, this means we've successfully blocked the packets using our firewall. YIPPEE!

![](https://github.com/mooroon/NetworkingA13/blob/main/IMAGES/Screenshot%20from%202024-05-08%2009-41-45.png)

### 5. Test IP protocol using the browser
Now we can see if we have successfully allowed the IP protocol

- Go to the web browser on your PC
- enter http://[ip address]
in our case it will look like this: http://10.13.10.1
![](https://github.com/mooroon/NetworkingA13/blob/main/IMAGES/Screenshot%20from%202024-05-08%2009-41-55.png)
![](https://github.com/mooroon/NetworkingA13/blob/main/IMAGES/Screenshot%20from%202024-05-08%2009-42-23.png)

There we go! We have created a basic network and utilised the server's in built firewall software to protect it. 

## Challenges
Try expanding the network, add more PCs, servers, and switches to the network. You could also introduce VLANs to seperate the parts of your network.

Explore using advanced/more sophisticated firewall rules to control more "traffic flow". For example, you may allow specific services from certain IP addresses or subnets while blocking others. Maybe try experimenting with different protocols and port numbers.
