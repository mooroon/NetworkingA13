# Firewalls

This recipe will help configure a  network that includes a firewall

## Topics covered

At the end of this recipe, you will know how to:
- Answer: What is a firewall?
- Answer: How do firewalls work?
- Build the following network and configure a firewall


## What is a Firewall?
How do you stop people from reaching internal systems that they aren’t supposed to? 
A firewall is a system that is designed to prevent unauthorised access from entering a private network. They block unwanted access and permits wanted access, it basically acts as a safety barrier between a private network and public entertainment.

## What is an ASA Firewall?
ASA is a type of firewall appliance developed by Cisco Systems. It combines the functionality of a firewall with other features such as VPN capabilities, intrusion prevention, content security, and identity-based access control. ASAs are often used in enterprise environments to provide comprehensive network security. They offer features like stateful inspection, application-layer filtering, and advanced threat protection to safeguard networks from various cyber threats. 


### Things you'll need to know before you start this

- [Ip Configuration](https://github.com/carteras/cookbook/blob/main/networks/000.hello_packettracer.md)

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

### 2. Configure all ip addresses and subnet masks of pcs and servers
![](https://github.com/mooroon/NetworkingA13/blob/main/IMAGES/Screenshot%20from%202024-05-08%2009-37-57.png)
![](https://github.com/mooroon/NetworkingA13/blob/main/IMAGES/Screenshot%20from%202024-05-08%2009-38-03.png)
### 3. go to ipv4 firewall on server's desktop
- make sure service is turned on
![](https://github.com/mooroon/NetworkingA13/blob/main/IMAGES/Screenshot%20from%202024-05-08%2009-38-49.png)
![](https://github.com/mooroon/NetworkingA13/blob/main/IMAGES/Screenshot%20from%202024-05-08%2009-39-48.png)
![](https://github.com/mooroon/NetworkingA13/blob/main/IMAGES/Screenshot%20from%202024-05-08%2009-40-48.png)
### 4. ping computer 
![](https://github.com/mooroon/NetworkingA13/blob/main/IMAGES/Screenshot%20from%202024-05-08%2009-41-45.png)
### 5. web browser
![](https://github.com/mooroon/NetworkingA13/blob/main/IMAGES/Screenshot%20from%202024-05-08%2009-41-55.png)
![](https://github.com/mooroon/NetworkingA13/blob/main/IMAGES/Screenshot%20from%202024-05-08%2009-42-23.png)
## Practice Questions
