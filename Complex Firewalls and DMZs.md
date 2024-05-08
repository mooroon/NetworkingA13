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
-[Firewall Intro](https://github.com/mooroon/NetworkingA13/blob/main/Firewall%20Intro.md)


## Instructions

Download the project from here: 

### 1. Create the following network
![](https://github.com/mooroon/NetworkingA13/blob/main/IMAGES/Screen%20Shot%202024-05-08%20at%208.41.11%20pm.png)



## Challenges
Try expanding the network, add more PCs, servers, and switches to the network. You could also introduce VLANs to seperate the parts of your network.

Explore using advanced/more sophisticated firewall rules to control more "traffic flow". For example, you may allow specific services from certain IP addresses or subnets while blocking others. Maybe try experimenting with different protocols and port numbers.
