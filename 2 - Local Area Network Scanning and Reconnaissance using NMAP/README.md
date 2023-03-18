## Use the tool NMAP [Command line only] to perform the below task. Run Wireshark in the background and capture only the necessary packets to showcase for the corresponding question.

## a) Explain the subnet and use the NMAP Command to scan the services for the whole subnet.

A subnet is a portion of a network that has been partitioned into smaller networks, each with its own unique IP address range. This is done to improve network performance, security, and manageability. Subnetting allows network administrators to divide a large network into smaller subnetworks, which can be used to group devices that have similar functions or security requirements.

Command to scan entire subnet - `nmap -sn <network address>/<subnet prefix/CIDR notation>`

Example - `nmap 192.168.1.0/24`

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
 

c) Use the NMAP command to scan a network and determine which devices are up and running.



d) What are vertical and horizontal scanning?

- `Vertical scanning`, also known as **service scanning**, involves **scanning a single host for all the open ports and services** that are running on it. This approach allows for a detailed analysis of the individual host, including the versions of services running, operating system, and other relevant information.

- `Horizontal scanning`, also known as **port scanning**, involves **scanning multiple hosts for a specific open port or set of ports**. This approach allows for a quick overview of the network or hosts that may have a specific service or vulnerability present.

e) Use the NMAP command to scan multiple hosts. [HINT: Add hosts into a file and scan it].

f) Use NMAP commands to export the output in XML format.

g) Use the NMAP command to get OS information about a host.

h) Explain ping sweeping and Perform ping sweeping using Nmap

#### Ping Sweep

Ping sweeping is a network reconnaissance technique used to determine which IP addresses are alive and responsive on a network. It involves sending a series of ICMP echo request messages, also known as pings, to a range of IP addresses, usually in a sequential order, to identify which ones are available and can be reached.

Ping sweeping is often used by network administrators to identify active hosts on a network and to map the network

Nmap command to perform ping sweep - `nmap -sn <network address>/<CIDR>`.

where,

`-sn` -  allows to perform a ping scan only on the target:



> Also, learn other scans of NMAP using the man page or –help option.
## Try these below questions after completing the above commands.

1. What is a web application firewall? How do you use Nmap to detect a WAF? Perform WAF
fingerprint detection using NMAP.

2. What is EXIF data? Try to find EXIF data of images on a website using NMAP NSE
3. Use NMAP NSE to find all subdomains of the website.
4. Perform a vulnerability scan on the target host using NMAP NSE.
