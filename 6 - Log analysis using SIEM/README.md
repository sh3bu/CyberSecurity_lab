## 1. Understand the architecture of Splunk and the installation process. Setup collector and forwarder, then ensure the logs are accumulated in Splunk. Familiarize yourself with the dashboard fields.

**Installation -**

![image](https://github.com/sh3bu/CyberSecurity_lab/assets/67383098/eb75c78f-6132-4ef2-a12c-ad8dc4dffd57)

**Start splunk instance -**

![image](https://github.com/sh3bu/CyberSecurity_lab/assets/67383098/95e0c63a-5717-41e5-9711-7b7205c4191e)

**Create credentials to loin t splunk forwarder -**

![image](https://github.com/sh3bu/CyberSecurity_lab/assets/67383098/cbec10cd-e377-4948-ab3f-a33cda1df4d2)

**Forward all logs to splunk enterprise which is located in our windows machine -**

![image](https://github.com/sh3bu/CyberSecurity_lab/assets/67383098/27f86ec8-9c3a-467e-afc1-8a61fc1cde0b)

**Use splunk add monitor to add the location of log files to be forwarded -**

![image](https://github.com/sh3bu/CyberSecurity_lab/assets/67383098/c67ec615-206e-483b-8c50-a7a2633d55b4)

**Start apache server to test and ensure if logs are being forwarded**

![image](https://github.com/sh3bu/CyberSecurity_lab/assets/67383098/7f0b01b8-2658-422a-9636-76212117e86a)

![image](https://github.com/sh3bu/CyberSecurity_lab/assets/67383098/c30bf234-d648-4d51-94bb-c7d137949b6c)

![image](https://github.com/sh3bu/CyberSecurity_lab/assets/67383098/f27d846b-2014-49c3-8a52-3530b9b0f0db)

![image](https://github.com/sh3bu/CyberSecurity_lab/assets/67383098/806da74d-4538-453f-914f-89420340d247)


![image](https://github.com/sh3bu/CyberSecurity_lab/assets/67383098/8f3f391e-a19d-4d74-9948-c836fd73d3fb)

Thus from the below screenshot we can confirm that our logs are being forwarded.

![image](https://github.com/sh3bu/CyberSecurity_lab/assets/67383098/2ea3fddc-a62d-4364-b57e-57fb951f9ec1)



## 2. Run Splunk >> Forwarder can be in the same system or another system (user’s convenience)
>>Make sure the logs are indexing in the Splunk enterprise.

```
• Run any network and port scanning commands from the host to the target machine.
Run at least 5 to 8 commands. (If required, any tools can also be used).

• Use the search section in Splunk to analyze the firewall logs to find the log of the above
process and the exact IP from where the scan was performed. HINT: Use the “stats”
command.

• Analyze the log file and create an alert for any further similar activities.
```

**Add thr location of folder where nmap log files are stored -**

![image](https://github.com/sh3bu/CyberSecurity_lab/assets/67383098/f9cc87de-f58b-4cb3-9f5b-d035fda84cab)

**Run nmap command on linux system - **

![image](https://github.com/sh3bu/CyberSecurity_lab/assets/67383098/8bd89654-888b-4c15-b540-1825ed800ed7)

**Perform search query**

![image](https://github.com/sh3bu/CyberSecurity_lab/assets/67383098/793e81f6-64b3-4feb-b2a2-549c9f71ac61)


## 3. Run Splunk >> Forwarder can be in the same system or another system (user’s convenience)

>>Make sure the logs are indexing in the Splunk enterprise.

```

• Perform any communication using unencrypted traffic.

• Use the Splunk search section to check the firewall logs to analyze which application
uses unencrypted data.

• Analyze the log file and create an alert for any further similar activities.
```

![image](https://github.com/sh3bu/CyberSecurity_lab/assets/67383098/449c416d-2def-45a6-9a92-ee6a879b0798)

![image](https://github.com/sh3bu/CyberSecurity_lab/assets/67383098/1a59aa5d-f334-4d4a-b61b-4d3de75f47da)


![image](https://github.com/sh3bu/CyberSecurity_lab/assets/67383098/8e7576be-2aa8-4a92-8265-68db9147f2f8)

![image](https://github.com/sh3bu/CyberSecurity_lab/assets/67383098/903884b6-0e0a-44ec-9c43-505b367b74ab)



## 4. Run Splunk >> Forwarder can be in the same system or another system (user’s convenience)

>>Make sure the logs are indexing in the Splunk enterprise. Download malware from this site


```
https://dasmalwerk.eu/ . CAUTION: THEY ARE REAL MALWARE. USE IN AN ISOLATED
ENVIRONMENT. >> Run the malware in your target system.

• After running your malware file, either it is stopped by your antivirus or not using the
search section, find the antivirus log for the past 1 hour.

• Run different malware files again in the same target system and use the search section
to find the time range between the previous and current malware file execution. HINT:
Use the “stats” command.

• Then save that search as an alert to show a notification when the same type happens
again.
```

## 5. Run Splunk >> Forwarder can be in the same system or another system (user’s convenience)

>>Make sure the logs are indexing in the Splunk enterprise.


```

• Logout of the target system and perform multiple failed attempts. Then use the search
section to filter out the failed attempt logs. Hint: Use the “stats” command.

• Analyze the log file and create an alert for any further similar activities
```

![image](https://github.com/sh3bu/CyberSecurity_lab/assets/67383098/4f4fc576-3b90-43f5-9b73-c0371816e178)

![image](https://github.com/sh3bu/CyberSecurity_lab/assets/67383098/e4964756-fdbc-44e9-8c30-8f14ba9b2b87)

