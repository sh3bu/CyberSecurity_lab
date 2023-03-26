# LAN based insider attacks


Make use of Ettercap/arpspoof tool to perform ARP Cache Poisoning based attacks in a LAN
environment:

## 1. Perform Password stealing (over plaintext) using ARP Cache Poisoning attacks

**Context -**

> ARP (Address Resolution Protocol) cache poisoning is a technique used by attackers to intercept network traffic between two hosts on a local network. In the context
> of ettercap, a popular network sniffing and MITM (Man-in-the-Middle) tool, the ARP cache poisoning plugin is used to perform this attack.
> When the ARP cache poisoning plugin is enabled in ettercap, it sends fake ARP messages to the hosts on the local network, which causes them to update their ARP cache
> with a fake MAC address for a particular IP address. This allows the attacker to intercept network traffic between two hosts on the local network by redirecting the
> traffic to their own machine.

For this attack we take 2 systems, 

- Kali (attacker) - 10.0.2.4
- Fedora (victim) - 10.0.2.5

First open `Ettercap` in kali linux

![image](https://user-images.githubusercontent.com/67383098/227707390-3f713cac-ab0d-49cf-b7ff-e9a0eb6071e1.png)

![image](https://user-images.githubusercontent.com/67383098/227707494-dee50bd4-2060-4b37-bc30-cacd7f567ba4.png)

Click on `hosts` -> `Scan for hosts`

![image](https://user-images.githubusercontent.com/67383098/227707588-259bf7ee-4b21-496f-acd7-bf9524a4b214.png)


![image](https://user-images.githubusercontent.com/67383098/227707616-48f7c6ec-6878-4e60-9140-05e3200411e5.png)

Add the ip address `10.0.2.5` as target.
Go to `MITM` -> select `arp poisoning`

![image](https://user-images.githubusercontent.com/67383098/227707736-b39fa6b7-5042-4297-8b85-0929575b5b16.png)

![image](https://user-images.githubusercontent.com/67383098/227707796-8adc7383-2049-4771-afdc-91a11afa2c4f.png)

Click **OK**. Now attack has started.

On attacker machine, open firefox & go to `testphp.vulnweb.com`

![image](https://user-images.githubusercontent.com/67383098/227707932-689b2035-4be9-4364-ace1-30abbe179712.png)

After we try to login with the credentials, we can see the packet being sniffed by ettercap in our kali attacker machine .

![image](https://user-images.githubusercontent.com/67383098/227708010-ebe6e2e4-8b17-4e59-acb5-67eb593e0326.png)




## 2. Perform Denial of Service (DoS) attacks using ARP Cache Poisoning attacks.

**Context -**

>  The DoS (Denial of Service) attack plugin in ettercap is used to flood a target system or network with an overwhelming amount of traffic to disrupt the normal
>  functioning of the system or network. The purpose of this attack is to make the target system or network unavailable to legitimate users.
>  The DoS attack plugin in ettercap works by generating a large amount of network traffic towards the target.
>  The legitimate traffic may include HTTP requests, DNS queries, or other network requests.

As like the previous steps, 

1. Scan for hosts
2. Add hosts as target (only the target ip & not the gateway ip)
3. Start arp poisoning the victim.

Now run the `dos_attack` plugin

![image](https://user-images.githubusercontent.com/67383098/227785280-253d3dad-7a57-4d1a-8713-fe4ddcfc53d6.png)

Enter the target ip.

![image](https://user-images.githubusercontent.com/67383098/227785325-9843ea75-cc93-4054-9a1b-d91a5c09750f.png)

Enter any unused ip in the subnetwork( ip which is not shownm in hosts list )

![image](https://user-images.githubusercontent.com/67383098/227786174-a01be130-3eaa-4f82-8c9e-7c9421d4f172.png)

Once we activate the plugin , the target ip sends hundreads of packets to victim, causing the victim to become slow. So any web search made by victim just keeps on loading.

![image](https://user-images.githubusercontent.com/67383098/227787244-41cda2ff-d2ee-475a-a283-8eda5bee6dc8.png)

## 3. Perform DNS Spoofing attack using ARP Cache Poisoning attacks

**Context -**

> When the DNS spoofing plugin is enabled in ettercap, it intercepts DNS queries from the victim and responds with a fake DNS response that contains a fake IP address. > This fake IP address is the IP address of the attacker's machine or any other IP address that the attacker wants the victim to visit.
> The ettercap DNS spoofing plugin listens for DNS requests made by the victim. Once a request is captured, the plugin sends a fake DNS response to the victim's
> machine, which contains the IP address of the attacker's machine or any other IP address specified by the attacker.

This manipulation of the DNS response allows the attacker to redirect the victim's traffic to any website or web page of their choice. Once the victim's traffic is redirected to the attacker's website, the attacker can then perform various malicious activities, such as stealing login credentials, injecting malware, or intercepting sensitive data.

Open ettercap. Go to `Plugins` -> `Hosts` -> `Scan for hosts` to scan all the hsots int he network.

Now click on `host list` to show the list of hosts identified.

Add the victim ip as target1 & gateway address as target2.

Open the ettercap config file which is located at `/etc/ettercap/etter.conf`

Change the following values to 0

![image](https://user-images.githubusercontent.com/67383098/227730162-ed9b4e48-e3ae-4e3a-89e8-efb694dc4f38.png)

Uncopmment the following lines

![image](https://user-images.githubusercontent.com/67383098/227730257-d4e9ca6e-cf51-4113-9423-d7ba513091b5.png)


Open the `etter.dns` file which is located at `/etc/ettercap/etter.dns`.

>` etter.dns` file is the hosts file and is responsible for redirecting specific DNS requests. Basically, if the target enters facebook.com they will be redirected to 
> Facebook's website, but this file can change

Type the following line  `google.com A 10.0.2.4 ` where 10.0.2.4 is the attacker ip

![image](https://user-images.githubusercontent.com/67383098/227732838-8729c151-af9d-4692-a8ea-03ab2db9fc63.png)

In a real life scenario, an attacker would use this attack to redirect traffic to their own machine for data sniffing. This is done by starting an Apache server on the Kali machine and changing the default homepage to a clone of, let's say facebook.com  so that when the victim visits those websites, after being redirected to the attacker machine they will see the clones of the aforementioned sites. This will probably fool the unsuspecting user into entering their credentials where they really shouldn't.


We setup a fake login page . Start the **apache2** server using the command `sudo systemctl start apache2`

![image](https://user-images.githubusercontent.com/67383098/227728008-785f27a3-e5f3-438f-830d-ec8e761bea37.png)

Go to ettercap -> `MITM` -> `ARP poisoning` -> choose `sniff remote connections` -> click `ok`

![image](https://user-images.githubusercontent.com/67383098/227728129-c06a3d1e-ef8e-4e8d-bb12-eaa9eb31b44b.png)

Activate the `dns_spoof` plugin by going to `plugins` -> `manage plugins` 

![image](https://user-images.githubusercontent.com/67383098/227732624-2399d27a-a0fa-4d73-bfb1-f60892df61d1.png)

The page ***mypage.io** is now mapped to 10.0.2.4 which is attacker 's IP address. 

So when victim types `mypage.io` he will be redirected to attacker's fake login page

![image](https://user-images.githubusercontent.com/67383098/227730302-1ed994d3-0ef7-4acf-8b12-40974b0892a6.png)





## 4. Invoke ‘sslstrip tool’ for stealing passwords from any machine that is connected to a LAN by stripping the HTTPS connection.

Sslstrip is a tool that can be used to perform a man-in-the-middle (MITM) attack on a network by intercepting HTTP traffic and downgrading HTTPS connections to plain HTTP. This means that the tool can be used to intercept sensitive information, including passwords, that would normally be encrypted and protected when transmitted over HTTPS.

## 5. Use arp_cop and scan_poisoner plugins to learn about the detection of ARP attacks.


Observe the ARP cache table, CAM table, etc., before and after the attack for all the above attacks. Run
Wireshark and observe the traffic patterns before and after the attack
