## 1. Learn the basic working of Wi-Fi and its types with various types of attacks on it.

To transmit and receive data wirelessly, Wi-Fi uses a wireless network adapter on each device, which converts the data into radio waves and sends them to the Wi-Fi router. The router then receives these radio waves and converts them back into data that can be sent to the internet or other devices on the network. Wi-Fi operates on different frequencies and channels, which determine the speed and range of the wireless connection.

- **Rogue access points** - attackers can set up a fake access point that appears to be legitimate, tricking users into connecting to it and giving away their sensitive information.

- **Man-in-the-middle attacks** - attackers intercept and alter data as it is transmitted between devices, allowing them to steal sensitive information.

- **Denial-of-service attacks** - attackers flood the Wi-Fi network with traffic, causing it to crash or become unusable.

- **Eavesdropping** - attackers can intercept and read data that is being transmitted between devices over the Wi-Fi network.

- **Password cracking** - attackers can use specialized software to crack the Wi-Fi network's password, giving them access to the network and any sensitive information transmitted over it.

----------------------

## 2. Perform Wi-Fi fingerprinting using Wigile, Inssider, and Kismet.

#### Wigle.net

![image](https://user-images.githubusercontent.com/67383098/230648536-6a44927f-60a6-4e94-9089-c879ae82fa29.png)

#### inSSIDer

![image](https://user-images.githubusercontent.com/67383098/230650197-3f7cce6f-a390-4d2a-b0b0-1dccb5f88427.png)


#### Kismet -

- Put Your Wireless Card in Monitor Mode by using the command `sudo airmon-ng start wlan0`

![image](https://user-images.githubusercontent.com/67383098/230551170-37f0d414-dd18-4c86-b728-5cfbacc2f2d3.png)

- Launch Kismet by using the command `kismet -c wlanomon`

![image](https://user-images.githubusercontent.com/67383098/230552556-1d7bd6a6-bc11-4152-9989-001327bbfb93.png)

Go to **localhost:2501** to view kismet page. Create a account with any password, in this case I created **username:kismet** & **password:kismet**

![image](https://user-images.githubusercontent.com/67383098/230552480-bdc61d8a-b846-4b13-a472-d352e2c0d806.png)

Here we can see the **SSID** & the type of encryption being used.

![image](https://user-images.githubusercontent.com/67383098/230552332-32a6be07-3554-4bff-9661-17fe92d3b727.png)

--------------------------------------------

## 3. Create an Access point with any Wi-Fi encryption standard and start testing the security ofthat connection using any Wi-Fi security testing tools, which should include (Aircrack-Ng, Wifite, not limited). Try to capture the 4-way handshake using these methods.

Start monitor mode - `airmon-ng start wlan0`

![image](https://user-images.githubusercontent.com/67383098/230554024-50eefd46-08d0-4e50-a525-dd92dec5881a.png)


Capture wireless traffice using - `airodump-ng wlan0`

![image](https://user-images.githubusercontent.com/67383098/230555155-dc581e48-5db2-4a9d-b319-0dd5f2197e66.png)

Focus Airodump-Ng on One AP on One Channel - `airodump-ng --bssid EA:B0:24:9F:4A:50  -c 5 --write WPAcrack wlan0`

It will capture and store all the files including .pcap file to the present directory which can later be used for bruteforcing  the password.

![image](https://user-images.githubusercontent.com/67383098/230556046-cc586b48-b820-4505-9169-646d9a28cff4.png)

Aireplay-Ng Deauth - `aireplay-ng --deauth 100 -a EA:B0:24:9F:4A:50 wlan0`

![image](https://user-images.githubusercontent.com/67383098/230556612-09f1a09a-3aa7-49f5-ad7f-7ad0435c226a.png)

Below is the captured **4 way handshake** during the deauth process

![image](https://user-images.githubusercontent.com/67383098/230556884-b437c7ae-6f60-4174-be73-a34409ed85ec.png)



----------------------------

## 4. After capturing the required files for testing, use dictionary generation and password cracking tools to crack the Wi-Fi password.
a. You must use an existing word file to crack the password.
b. Also you have to create your dictionary file for cracking the passwords.
c. Keep 3 different types of passwords for your Wi-Fi to test it. Simple, medium, and
complex passwords can be used for testing. Simple can be a dictionary word,
medium can be of dictionary word with some numbers, and complex can be
generated from any password generator online.

Password is `c6dp6m2k`

Now first we try to crack a hard password which was set as password for the  Wifi AP named *realme 10 pro 5g* where password is `c6dp6m2k`

Command - `aircrack-ng WPAcrack-03.cap  -w /usr/share/wordlists/rockyou.txt`

![image](https://user-images.githubusercontent.com/67383098/230557921-fe84d8c4-95d1-48c9-b34d-eb4152d05847.png)

When we use a weak password, we can crack it in less time using aircrack-ng. (REPEAT ALL THE PROCESS ABOVE AND CAPTURE THE TRAFFIC)

aircrack-ng testt.cap -w /usr/share/wordlists/rockyou.txt

![image](https://user-images.githubusercontent.com/67383098/230582697-1c10599d-ef77-4013-b14d-f184c284929d.png)

As seen above , we have our password for the wifi AP which has WPA2 encryption which is **raymond23**

--------------------------

## 5. Use Rouge AP (WifiPhisher) to create an Evil twin, perform a basic phishing attack using this
rouge AP, and document the difference between the two attacks you have performed.

------------------------------

## 6. Learn the protocol level working of WPA3 and how it differs from WPA2.

WPA3 (Wi-Fi Protected Access III) is the latest security protocol for Wi-Fi networks, introduced by the Wi-Fi Alliance in 2018. It is designed to improve the security and privacy of Wi-Fi networks, addressing some of the vulnerabilities and weaknesses of its predecessor, WPA2. It uses a stronger authentication method, stronger encryption, and forward secrecy. It also includes a new feature to improve the security of public Wi-Fi networks. These improvements make it more difficult for attackers to gain unauthorized access to Wi-Fi networks and intercept data transmitted over them, providing a higher level of security for users.

Authentication: WPA3 uses a new authentication method called Simultaneous Authentication of Equals (SAE), also known as Dragonfly. This replaces the pre-shared key (PSK) method used in WPA2, which is vulnerable to brute force attacks. SAE is a stronger form of password-based authentication, which uses a cryptographic algorithm to protect against these types of attacks.

Encryption: WPA3 uses 256-bit Galois/Counter Mode Protocol (GCMP-256) encryption, which is more secure than the Advanced Encryption Standard (AES) encryption used in WPA2. GCMP-256 provides stronger protection against unauthorized access and data interception, as well as reducing the risk of side-channel attacks.

Forward Secrecy: WPA3 also includes support for Forward Secrecy, which generates a unique key for each session between a client and the access point. This makes it more difficult for an attacker to access past communications even if they are able to obtain the key used for the current session.

Public Wi-Fi Security: WPA3 includes a new feature called Opportunistic Wireless Encryption (OWE), which is designed to improve the security of public Wi-Fi networks. OWE encrypts data exchanged between a user and a Wi-Fi access point, even if the user doesn't have a password for the network. This helps protect against unauthorized access and data interception on public Wi-Fi networks.



Reference Links:
1. https://github.com/wifiphisher/wifiphisher
2. https://web.stanford.edu/class/ee26n/Assignments/Assignment7.html
3. https://www.wifi-professionals.com/2019/01/4-way-handshake
4. https://nooblinux.com/crack-wpa-wpa2-wifi-passwords-using-aircrack-ng-kali-linux/
5. https://en.wikipedia.org/wiki/IEEE_802.11

