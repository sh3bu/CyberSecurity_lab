## Use the tool NMAP [Command line only] to perform the below task. Run Wireshark in the background and capture only the necessary packets to showcase for the corresponding question.

## a) Explain the subnet and use the NMAP Command to scan the services for the whole subnet.

A subnet is a portion of a network that has been partitioned into smaller networks, each with its own unique IP address range. This is done to improve network performance, security, and manageability. Subnetting allows network administrators to divide a large network into smaller subnetworks, which can be used to group devices that have similar functions or security requirements.

Command to scan entire subnet - `nmap -sn <network address>/<subnet prefix/CIDR notation>`

Example - `nmap 192.168.1.0/24`

![image](https://user-images.githubusercontent.com/67383098/226188623-ec2bed0f-0a5a-4337-9dc8-0f8c349c9363.png)


## b) What is a firewall and mention its types. Use the NMAP command to detect that a firewall protects the host.

#### Firewall 

- A firewall is a network security device that monitors and controls incoming and outgoing network traffic based on a set of predefined security rules. Its primary purpose is to protect networks and devices from unauthorized access, attacks, and malicious activity.
- Firewalls can be implemented as software, hardware, or a combination of both. They work by examining the packets of network traffic and comparing them against the set of rules or policies defined by the administrator. 
- If a packet matches a rule, it is allowed to pass through the firewall. If it doesn't match any rule, it is either dropped or sent to a different location for further analysis

#### Types

- Packet filtering firewall
- Stateful inspection firewall
- Application-level gateway firewall
- Next-generation firewall
- Host-based firewall

#### nmap command to identify a firewall - 
To identify a firewall we can use the `Standard SYN Scan`

> Reason : The RST packet makes closed ports easy for Nmap to recognize. Filtering devices such as firewalls, on the other hand, tend to drop packets destined for
> disallowed ports. In some cases they send ICMP error messages (usually port unreachable) instead. Because dropped packets and ICMP errors are easily distinguishable > from RST packets, Nmap can reliably detect filtered TCP ports from open or closed ones, and it does so automatically.

Command - `nmap -sS -p- <ip>`
>  If a port is filtered by a firewall, Nmap will not be able to determine if it is open or closed, but will instead report it as "filtered"


 where,
 
 `-sS` - SYN scan
 
 `-p-` -  all ports
 
![image](https://user-images.githubusercontent.com/67383098/226191049-d321a20b-4e16-404f-9c22-721bbbd2d1cf.png)

## c) Use the NMAP command to scan a network and determine which devices are up and running.

Command - `nmap -sn <ip>/<CIDR> `

![image](https://user-images.githubusercontent.com/67383098/226189218-0674b7bb-1822-440b-a54c-e2bc3180a5d7.png)


## d) What are vertical and horizontal scanning?

- `Vertical scanning`, also known as **service scanning**, involves **scanning a single host for all the open ports and services** that are running on it. This approach allows for a detailed analysis of the individual host, including the versions of services running, operating system, and other relevant information.

- `Horizontal scanning`, also known as **port scanning**, involves **scanning multiple hosts for a specific open port or set of ports**. This approach allows for a quick overview of the network or hosts that may have a specific service or vulnerability present.

## e) Use the NMAP command to scan multiple hosts. [HINT: Add hosts into a file and scan it].

Adding the ip address to `/etc/hosts` file.

![image](https://user-images.githubusercontent.com/67383098/226190526-521b91db-c0da-4e70-bd8d-f1f85fa4a14a.png)

![image](https://user-images.githubusercontent.com/67383098/226190608-4ddacc0b-c8b6-4104-a26a-d1f90818f9b3.png)


## f) Use NMAP commands to export the output in XML format.

For this we use the `-oX` flag.

EX - `nmap -sCV` <target-ip> -oX result.xml`
 
![image](https://user-images.githubusercontent.com/67383098/226130386-8fa39901-e04f-480c-b0a5-241326d28479.png)


## g) Use the NMAP command to get OS information about a host.
 

To find the OS information about the host, we use the `-O` flag .

EX - `nmap -O <target-ip>`

![image](https://user-images.githubusercontent.com/67383098/226191577-8674c6f3-e5f8-433d-bd5e-4fb13df68331.png)


## h) Explain ping sweeping and Perform ping sweeping using Nmap

#### Ping Sweep

Ping sweeping is a network reconnaissance technique used to determine which IP addresses are alive and responsive on a network. It involves sending a series of ICMP echo request messages, also known as pings, to a range of IP addresses, usually in a sequential order, to identify which ones are available and can be reached.

Ping sweeping is often used by network administrators to identify active hosts on a network and to map the network

Nmap command to perform ping sweep - `nmap -sn <network address>/<CIDR>`.

where,

`-sn` -  allows to perform a ping scan on the target:

![image](https://user-images.githubusercontent.com/67383098/226191763-07d7092c-12ef-495c-b49c-8d065e2c8ed8.png)


## Try these below questions after completing the above commands.

## 1. What is a web application firewall? How do you use Nmap to detect a WAF? Perform WAF fingerprint detection using NMAP.

- A **web application firewall (WAF)** is a firewall that monitors, filters and blocks data packets as they travel to and from a website or web application. 

 - A WAF can be either network-based, host-based or cloud-based and is often deployed through a reverse proxy and placed in front of one or more websites or applications. 
 
- Running as a network appliance, server plugin or cloud service, the WAF inspects each packet and uses a rule base to analyze Layer 7 web application logic and filter out potentially harmful traffic that can facilitate web exploits.
 
 Command - `nmap --script http-waf-detect`
 
 ![image](https://user-images.githubusercontent.com/67383098/226195021-db8e14c3-f334-4633-ab66-c15e572200cd.png)

 
## 2. What is EXIF data? Try to find EXIF data of images on a website using NMAP NSE

#### EXIF DATA 

- It  is a metadata that is embedded within image files, such as JPEGs, TIFFs, and RAW files. This data includes information about the camera settings used to take the picture, as well as information about the date, time, and location of the image
- Exif data can also include information about the camera's make and model, the lens used, and the exposure settings, such as shutter speed, aperture, and ISO.

 ![image](https://user-images.githubusercontent.com/67383098/226196247-166ac25b-8283-4037-8a8c-14bfc8813f6a.png)

 
## 3. Use NMAP NSE to find all subdomains of the website.

All the nse scripts are loacated in `/usr/share/nmap/scripts/`

> The `dns-brute` script built into Nmap is designed to enumerate subdomains and their corresponding server IP addresses.

![image](https://user-images.githubusercontent.com/67383098/226129157-fa9e31ae-c8b9-4dfa-ae95-e6ff37ce5490.png)


## 4. Perform a vulnerability scan on the target host using NMAP NSE.

Command -  `nmap -sV --script=vuln <target ip>`

![image](https://user-images.githubusercontent.com/67383098/226194429-7be73c14-e520-4dbf-ad20-13e96aa1c6dd.png)
 
![image](https://user-images.githubusercontent.com/67383098/226194499-d4316864-5339-4cdc-8e95-f9e541422f16.png)


