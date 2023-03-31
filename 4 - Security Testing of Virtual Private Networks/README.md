1. Create an IPsec-based VPN with the help of the Strongswan tool. 

a. Configure it with IKE version 1, perform the pen-testing procedures, and make it to 
IKE version 2 and follow the same. Add your observations to the report. 

![image](https://user-images.githubusercontent.com/67383098/228595143-14e8886f-aea1-405b-b954-e9784a8382ca.png)

```
┌──(root㉿kali)-[~]
└─# sysctl -p                 
net.ipv4.ip_forward = 1
net.ipv6.conf.all.forwarding = 1
net.ipv4.conf.all.accept_redirects = 0
net.ipv4.conf.all.send_redirects = 0

```

![image](https://user-images.githubusercontent.com/67383098/229168161-1c8b1630-90cb-4392-be47-2344cc6a0854.png)

![image](https://user-images.githubusercontent.com/67383098/229168361-d11a10bf-8091-4d80-bb86-da3e674f40d3.png)

![image](https://user-images.githubusercontent.com/67383098/229168978-e864a4ae-5119-452f-ad19-5d06d006cffd.png)
![image](https://user-images.githubusercontent.com/67383098/229169056-7bfc95b2-3c16-49c5-b9e9-6b75387fce64.png)


![image](https://user-images.githubusercontent.com/67383098/229172238-737294cb-a517-4127-be0f-2d5d3da0a629.png)
![image](https://user-images.githubusercontent.com/67383098/229172303-e9e19ffc-6327-48ac-ab4e-18341c9d9ef6.png)

![image](https://user-images.githubusercontent.com/67383098/229173137-c973e4ba-9cf5-423f-bd55-b5f5b0a493b9.png)
![image](https://user-images.githubusercontent.com/67383098/229173217-a9b50e78-5ac4-44a1-a811-ac00da4c62c0.png)



b. Configure your PSK to your own key phrase, then try to crack it offline. Then follow
the same by creating a random auto-generated PSK and try the same. 
Reference link: https://www.tecmint.com/setup-ipsec-vpn-with-strongswan-ondebian-ubuntu/

--------------------------------------------------------------------

2. Pen testing parameters for VPN: 
a. Scanning or identifying the VPN gateway.
b. Fingerprinting the VPN gateway for guessing implementation.
c. PSK mode assessment and PSK sniffing.
d. Offline PSK cracking.
e. Checking for default user accounts.
f. Testing the VPN gateway for vendor-specific vulnerabilities.
g. Check is there any firewall is present in this network before VPN. 
h. Perform necessary IKE scans
Reference Link : https://doxsec.wordpress.com/2015/08/07/ipsec-vpn-penetrationtesting-with-backtrack-and-kali-linux-tools/


-----------------------------------------------------------------------

3. Create a professional pen test report for your above findings. You can refer to the sample 
template attached. 
Template link: https://www.hackthebox.com/storage/press/samplereport/samplepenetration-testing-report-template.pd
