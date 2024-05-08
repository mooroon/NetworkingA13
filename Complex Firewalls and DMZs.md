# Complex Firewalls and DMZs

This lesson will expand on knowledge of firewalls and introduce the idea of a DMZ. This lesson will start easy and get progressively harder. This project doesn't have tests/marking on packet tracer as it is intended to be a bit of a play space. 

## Topics covered

At the end of this lesson, you will know:
- What a DMZ is
- How to build a network using DMZs and firewalls
- How to configure firewalls to create a DMZ

## Key Terms
- DMZ
- ASA
- AAA
- SSH Configuration
- SSH Timeout
SSH timeouts are the maximum amount of time that an SSH session can remain idle or inactive before it is closed by either the client or the server
- RSA Key Pair
An RSA key pair consists of a public key and a private key used in asymmetric cryptography. The keys are generated using prime numbers, and the security relies on the difficulty of factoring large composite numbers. The public key is used for encryption, while the private key is used for decryption.

## What is a DMZ?
DMZ stands for demilitarised zone

DMZs are useful for protecting "networks"/hosts from malicious threats but still allowing a limited access to and from the interent. DMZs have a different level of security than the remainder of a "network". 

## How Do DMZs Work?
DMZs refers to segments of a network created between an external network like the internet and an internal network such as an internal LAN. Normally, the DMZ is isolated from the external network, the Internet, and the internal network by a firewall. By installing a server that is open to the public, such as a web server, in the DMZ, even if there is unauthorized access from the outside, the network is isolated, and therefore, a security effect can be expected. This will provide a security effect even if there is unauthorized access from the outside

For example in the previous lesson our network had a security level of 100 but a DMZ may have a security level of 50. When we assign security levels, we assign them to interfaces, not networks. However, in this lesson there will still be references to assigning security levels to networks for simplicity's sake. 




### Recommended Knowledge 
-[Firewall Intro](https://github.com/mooroon/NetworkingA13/blob/main/Firewall%20Intro.md)


## Instructions
Canberra College needs your help! There are rumours about a security threat coming from an outside network and you need to help stop it. You don't know much about the threat but what you do know is that your networking class can be trusted and the other networking class can be partially trusted but you need to keep an eye out. From what you've heard, the drama faculty wants your classroom as a rehearsal space and will go to any lengths to compromise it. You have been informed that you have to limit their access but not completely or they will get suspicious. You suspect a DMZ allowed by a firewall, using the other networking class' network will do the trick. 

Download the project from here: 

### 1. Connect them All Together

Connect the firewall to each network but do not connect the networks to each other.

What we have done is ensured that any packets passed from one network to another must go through the firewall and run through the policies we are about to configure.

### 2. 
- Go to CLI
- Input following commands:

```cmb

ciscoasa>enable
Password: (We don't have a password yet so just hit enter)
ciscoasa#configure terminal
ciscoasa(config)#hostname PERIMETER-FW

```
Here we are enabling access and setting a meaningful hostname, next up is setting a password

```cmb

PERIMETER-FW(config)#enable password emilyisthebest
PERIMETER-FW(config)#username emily password emilyisthebest
PERIMETER-FW(config)#clock set 23:17:30 8 May 2024

```
We have also set a time and date so we can keep track of what is happening when, it might come in handy when observing traffic flow and monitoring activity. Make sure your password is secure, I have used a fairly obvious one to demonstrate but make sure you don't use such a widely agreed upon statement or it might be guessed easily.

```cmb

PERIMETER-FW(config)#interface gig1/1
PERIMETER-FW(config-if)#no shutdown
PERIMETER-FW(config-if)#ip address 10.13.10.13 255.255.255.0
PERIMETER-FW(config-if)#nameif LINETWO
PERIMETER-FW(config-if)#security-level 100
PERIMETER-FW(config-if)#exit

```

What has just been done is we have named our inside network and given it a security level of 100. Security level refers to how much you trust a network, 100 being most and 0 being least. Continue with other networks.

```cmb

PERIMETER-FW(config)#interface gig1/2
PERIMETER-FW(config-if)#no shutdown
PERIMETER-FW(config-if)#ip address 10.13.10.10 255.255.255.240
PERIMETER-FW(config-if)#nameif DMZ
PERIMETER-FW(config-if)#security-level 70
PERIMETER-FW(config-if)#exit

```
We have now set up our demilitarised zone, yippee. The DMZ has been given a security level of 70 because it is only partially trusted. Now for the last network.

```cmb

PERIMETER-FW(config)#interface gig1/3
PERIMETER-FW(config-if)#no shutdown
PERIMETER-FW(config-if)#ip address 198.164.10.13
PERIMETER-FW(config-if)#nameif OUTSIDE
PERIMETER-FW(config-if)#security-level 0
PERIMETER-FW(config-if)#exit

```

The outside network has been given a 0 security level because we do not trust them at all. Before we forget, make sure to save your changes and then display them to check that everything is in order

```cmb

PERIMETER-FW(config)#write memory
PERIMETER-FW(config)#show start

```

### 3. Cisco ASA Firewall as the DHCP Server
We will now use the ASA Firewall as a DHCP server but only for our trusted network
- Click on Firewall
- Open CLI again

```cmb

PERIMETER-FW(config)#dhcpd address 10.13.10.130-10.13.10.160
PERIMETER-FW(config)#dhcpd address 10.13.10.130-10.13.10.160 LINETWO
PERIMETER-FW(config)#dhcpd dns 8.8.8.8
PERIMETER-FW(config)#dhcpd enable LINETWO
PERIMETER-FW(config)#write memory
PERIMETER-FW(config)#show start

```

### 4. Set all IPs
Assign all g0/1 Devices to DHCP ip addresses instead of static ones. You can then ping other PCs in the network using the command line.

```cmb

C:\>ping 10.13.10.131

```

### 5. SSH Configuration
We are going to enable local aaa authentication for username to SSH onto ASA, we do this by once again going into CLI in the firewall

```cmb

PERIMETER-FW(config)#aaa authentication ?
PERIMETER-FW(config)#aaa authentication ssh ?
PERIMETER-FW(config)#aaa authentication ssh console
PERIMETER-FW(config)#aaa authentication ssh LOCAL

```
This means we are going to use the local database which includes the username and password we created in the previous steps

### 6. Generate RSA Key Pair

```cmb

PERIMETER-FW(config)#crypto key generate rsa modulus 1024
yes

```

### 7. Defining allowed IPs and subnets
We only want our inside network to be able to log in to the firewall. You can define the whole network as a group ordefine specific IP addresses to remotely access the firewall. We are going to allow the whole group

```cmb

PERIMETER-FW(config)#ssh ?
PERIMETER-FW(config)#ssh 10.13.10.13 255.255.255.0 LINETWO
PERIMETER-FW(config)#ssh timeout ?
PERIMETER-FW(config)#ssh timeout 3
PERIMETER-FW(config)#write memory

```
We have now allowed all of the LINETWO network to remotely access the firewall and set a time limit of 3 minutes before ssh timeout. We can test our work by logging into the firewall via a PC from the network using the command line.


ssh -1 emily 10.13.10.13
Password: emilyisthebest


Once you are in, you can execute several commands. You can attempt to do the same thing from a different network and hopefully you will not be able to get in. 


## Challenge
Try integrating elements from the Firewall Intro lesson to create another layer of security for the inside network by using software firewalls.




