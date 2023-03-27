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


> The purpose of SSLstrip is to perform a man-in-the-middle (MitM) attack to intercept and modify HTTP traffic that should be protected by SSL/TLS encryption.

> When a user visits a website that uses SSL/TLS encryption, their browser should establish a secure HTTPS connection to the server. However, SSLstrip can intercept
> the user's initial HTTP request and modify it so that it appears to be a non-secure HTTP request instead. The plugin can then forward this request to the server and
> intercept any response that the server sends back.

We need to change the value of this file `/proc/sys/net/ipv4/ip_forward`  from **0** to **1**
 
![image](https://user-images.githubusercontent.com/67383098/227924967-0decfc94-a0d5-439e-85ea-1797718ecc08.png)

Scan the hosts for systems that are alive in the network. Add te gateway address as target1 & victim ip as target2.

![image](https://user-images.githubusercontent.com/67383098/227925428-3f77757a-1005-45c3-b1e1-e411977006c8.png)

Activate `sslstrip` plugin 

![image](https://user-images.githubusercontent.com/67383098/227925578-a67e776a-e7a6-41bd-8496-9c78ee126599.png)

Go to `MITM` -> select `SSL Intercept`.

![image](https://user-images.githubusercontent.com/67383098/227925720-e5a7664a-8b8b-48f6-b12c-f270cc95f2c9.png)

Now sslstip plugin has been enabled.

![image](https://user-images.githubusercontent.com/67383098/227926008-cdfe03af-8834-41c4-8b87-e5811de9a53d.png)

Start arp_poisoning attack.


![image](https://user-images.githubusercontent.com/67383098/227926453-318d41ef-cf79-4b06-b6d8-09f5bf03180c.png)


Now in the victim, if we open a website we  will get **Secure connection failed** ie  ssl has been stripped. The page does not load because of ssl certificate mismatch error.

![image](https://user-images.githubusercontent.com/67383098/227926632-b7a9e41a-743e-470b-808f-094e159562ae.png)

I we disable the ssltrip plugin, then the page can load with https in victim machine.

![image](https://user-images.githubusercontent.com/67383098/227928211-a22eb879-3eaa-4a5d-b7b6-ab27b67c7a7b.png)

![image](https://user-images.githubusercontent.com/67383098/227928268-9ff4a119-40c0-4dcb-a052-843a3def0380.png)





## 5. Use arp_cop and scan_poisoner plugins to learn about the detection of ARP attacks.

> The arp_cop plugin is used to detect and prevent ARP spoofing attacks on a local network. It does this by monitoring ARP traffic on the network and comparing the MAC
> addresses associated with each IP address. If it detects a mismatch, indicating an ARP spoofing attack.

> The scan_poisoner plugin is used to automate ARP spoofing attacks on a network. It works by scanning the network for devices and their associated IP and MAC 
> addresses, and then sending ARP packets to associate the attacker's MAC address with each device's IP address. This allows the attacker to intercept and modify
> network traffic between each device and the rest of the network.

![image](https://user-images.githubusercontent.com/67383098/227937619-4588bec8-54b1-4b57-8a6b-439a59141420.png)



![image](https://user-images.githubusercontent.com/67383098/227937228-e8a35f79-8c17-4ab9-872f-8e79551f72d9.png)

![image](https://user-images.githubusercontent.com/67383098/227938566-5eb335d5-2127-4ffd-8f62-b64c62af5b2d.png)


![image](https://user-images.githubusercontent.com/67383098/227938135-8cd9320d-cfd9-494f-9058-97fab558498d.png)


**scan_poisoner**

Scan for hosts  in the network & create a host list.

Then activate `scan_poisoner` plugin

![image](https://user-images.githubusercontent.com/67383098/227951618-61d445d6-ab10-4e90-b46d-6e0eb09bc48d.png)

It shows nothing strange as of now. After we start an attack from the victim machine, it changes.

Add target 1 as gateway ip and target2 as attacker machine ip.

![image](https://user-images.githubusercontent.com/67383098/227956359-0682cbd5-8815-4228-a026-92e70e742abb.png)


Now in atttacker machine it shows the poisoners
![image](https://user-images.githubusercontent.com/67383098/227956863-ca1c742d-f083-4bb2-b74d-1511010be3c6.png)























Observe the ARP cache table, CAM table, etc., before and after the attack for all the above attacks. Run
Wireshark and observe the traffic patterns before and after the attack

BEFORE - 

![image](https://user-images.githubusercontent.com/67383098/227957565-20e57179-b66d-4e3c-88cb-980ed175d7fa.png)


AFTER - 

![image](https://user-images.githubusercontent.com/67383098/227957473-ab391511-0c14-4cc7-b372-c1ee94ff4076.png)
