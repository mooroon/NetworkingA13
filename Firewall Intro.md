# Firewalls

This lesson will help you to configure a network that includes a firewall.

*Keep in mind that the images may not show correct IP addresses and subnet masks, follow instructions in the packet tracer files or what is written in this file.*

## Topics covered

At the end of this lesson, you will know how to:
- Answer: What is a firewall?
- Answer: How do firewalls work?
- Build a network and configure a firewall


## What is a Firewall?
How do you stop people from reaching internal systems that they aren’t supposed to? 
A firewall is a system that is designed to prevent unauthorised access from entering a private network. They block unwanted access and permit wanted access, they basically act as a safety barrier between a private network and public entertainment.

## What is an ASA Firewall?
ASA is a type of firewall appliance developed by Cisco Systems. It combines the functionality of a firewall with other features such as VPN capabilities, intrusion prevention, content security, and identity-based access control. ASAs are often used in enterprise environments to provide comprehensive network security. They offer features like stateful inspection, application-layer filtering, and advanced threat protection to safeguard networks from various cyber threats. 


### Things you'll need to know before you start this

- [Basic Networking](https://github.com/carteras/cookbook/blob/main/networks/000.hello_packettracer.md)

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
