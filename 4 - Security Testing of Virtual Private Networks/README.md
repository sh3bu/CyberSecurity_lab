# IPSEC VPN

![image](https://user-images.githubusercontent.com/67383098/233851779-6b5307ec-0d6d-4385-a016-22f74eae5f4e.png)




## 1. Create an IPsec-based VPN with the help of the Strongswan tool. 

#### a. Configure it with IKE version 1, perform the pen-testing procedures, and make it to 
IKE version 2 and follow the same. Add your observations to the report. 

**Machine 1 - Ubuntu  - 192.168.180.209- devgateway1**

**Machine 2 - Kali    - 192.168.180.228 - devgateway2**

Make the following changes changes to `/etc/sysctl.conf`. Type **sysctl -p** to view the changes made

```
┌──(root㉿kali)-[~]
└─# sysctl -p                 
net.ipv4.ip_forward = 1
net.ipv6.conf.all.forwarding = 1
net.ipv4.conf.all.accept_redirects = 0
net.ipv4.conf.all.send_redirects = 0

```

Make changes to `/etc/ipsec.conf` in both the machines. Change the leftsubnet=<ip-of-machine1>, rightsubnet=,<ip-of-machine2> , keyexchange=ikev1/2

**Machine 1**
``` 
config setup
        charondebug="all"
        uniqueids=yes
conn devgateway1
        type=tunnel
        auto=start
        keyexchange=ikev1
        authby=secret
        left=192.168.180.209
        # leftsubnet=192.168.0.101/24
        right=192.168.180.228
        # rightsubnet=10.0.2.15/24
        ike=aes256-sha1-modp1024!
        esp=aes256-sha1!
        aggressive=no
        keyingtries=%forever
        ikelifetime=28800s
        lifetime=3600s
        dpddelay=30s
        dpdtimeout=120s
        dpdaction=restart
```
**Machine 2**
``` 
config setup
        charondebug="all"
        uniqueids=yes
conn devgateway2
        type=tunnel
        auto=start
        keyexchange=ikev1
        authby=secret
        left=192.168.180.209
        # leftsubnet=192.168.0.101/24
        right=192.168.180.228
        # rightsubnet=10.0.2.15/24
        ike=aes256-sha1-modp1024!
        esp=aes256-sha1!
        aggressive=no
        keyingtries=%forever
        ikelifetime=28800s
        lifetime=3600s
        dpddelay=30s
        dpdtimeout=120s
        dpdaction=restart
```

Make changes to `/etc/ipsec.secrets` config file in both machines.

```
root@ubuntu:/home/ubuntu# cat /etc/ipsec.secrets

# This file holds shared secrets or RSA private keys for authentication.
# RSA private key for this host, authenticating it to any other host
# which knows the public part.
#------- Site 1 Gateway (tecmint-devgateway) ------- 


192.168.180.209 192.168.180.228 : PSK "1234"
```

![image](https://user-images.githubusercontent.com/67383098/232959470-9ca42f62-42e6-48f3-96aa-665a2ccdf992.png)

Now using `ipsec up <gateway-name>` , we can establish the vpn connection between two machines.

![image](https://user-images.githubusercontent.com/67383098/232960104-ea9eb191-48d5-474d-9aa3-9e34ec05d488.png)

We send a msg from one machine to another and capture the packets in wireshark,

![image](https://user-images.githubusercontent.com/67383098/232960642-2dff575d-6d30-4db6-b41c-0c5312e6531d.png)

![image](https://user-images.githubusercontent.com/67383098/232960848-b7ef0876-bccc-4433-adeb-8e2a58aa0087.png)



b. Configure your PSK to your own key phrase, then try to crack it offline. Then follow
the same by creating a random auto-generated PSK and try the same. 
Reference link: https://www.tecmint.com/setup-ipsec-vpn-with-strongswan-ondebian-ubuntu/

--------------------------------------------------------------------

## 2. Pen testing parameters for VPN: 


#### NMAP

**Detecting whether the port is open/not**

![image](https://user-images.githubusercontent.com/67383098/233851506-3b2d8688-da6b-466a-b834-9f5b188218a1.png)


**OS detection**

![image](https://user-images.githubusercontent.com/67383098/233851281-f4621f8b-4e01-4c0b-acbb-735f2a105159.png)

**Vuln scan**

![image](https://user-images.githubusercontent.com/67383098/233851387-c0b14921-d116-4ba8-8fbd-0898b711f9a5.png)



-----------------------------------------------------------------------

3. Create a professional pen test report for your above findings. You can refer to the sample 
template attached. 
Template link: https://www.hackthebox.com/storage/press/samplereport/samplepenetration-testing-report-template.pd
