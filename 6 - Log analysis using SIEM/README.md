1. Understand the architecture of Splunk and the installation process. Setup collector and
forwarder, then ensure the logs are accumulated in Splunk. Familiarize yourself with the
dashboard fields.

![image](https://github.com/sh3bu/CyberSecurity_lab/assets/67383098/eb75c78f-6132-4ef2-a12c-ad8dc4dffd57)


![image](https://github.com/sh3bu/CyberSecurity_lab/assets/67383098/95e0c63a-5717-41e5-9711-7b7205c4191e)

![image](https://github.com/sh3bu/CyberSecurity_lab/assets/67383098/cbec10cd-e377-4948-ab3f-a33cda1df4d2)

![image](https://github.com/sh3bu/CyberSecurity_lab/assets/67383098/27f86ec8-9c3a-467e-afc1-8a61fc1cde0b)

![image](https://github.com/sh3bu/CyberSecurity_lab/assets/67383098/c67ec615-206e-483b-8c50-a7a2633d55b4)

![image](https://github.com/sh3bu/CyberSecurity_lab/assets/67383098/7f0b01b8-2658-422a-9636-76212117e86a)

![image](https://github.com/sh3bu/CyberSecurity_lab/assets/67383098/c30bf234-d648-4d51-94bb-c7d137949b6c)

![image](https://github.com/sh3bu/CyberSecurity_lab/assets/67383098/f27d846b-2014-49c3-8a52-3530b9b0f0db)

![image](https://github.com/sh3bu/CyberSecurity_lab/assets/67383098/806da74d-4538-453f-914f-89420340d247)


![image](https://github.com/sh3bu/CyberSecurity_lab/assets/67383098/8f3f391e-a19d-4d74-9948-c836fd73d3fb)

![image](https://github.com/sh3bu/CyberSecurity_lab/assets/67383098/2ea3fddc-a62d-4364-b57e-57fb951f9ec1)



2. Run Splunk >> Forwarder can be in the same system or another system (user’s convenience)
>>Make sure the logs are indexing in the Splunk enterprise.
• Run any network and port scanning commands from the host to the target machine.
Run at least 5 to 8 commands. (If required, any tools can also be used).
• Use the search section in Splunk to analyze the firewall logs to find the log of the above
process and the exact IP from where the scan was performed. HINT: Use the “stats”
command.
• Analyze the log file and create an alert for any further similar activities.


3. Run Splunk >> Forwarder can be in the same system or another system (user’s convenience)
>>Make sure the logs are indexing in the Splunk enterprise.
• Perform any communication using unencrypted traffic.
• Use the Splunk search section to check the firewall logs to analyze which application
uses unencrypted data.
• Analyze the log file and create an alert for any further similar activities.


4. Run Splunk >> Forwarder can be in the same system or another system (user’s convenience)
>>Make sure the logs are indexing in the Splunk enterprise. Download malware from this site
https://dasmalwerk.eu/ . CAUTION: THEY ARE REAL MALWARE. USE IN AN ISOLATED
ENVIRONMENT. >> Run the malware in your target system.
• After running your malware file, either it is stopped by your antivirus or not using the
search section, find the antivirus log for the past 1 hour.
• Run different malware files again in the same target system and use the search section
to find the time range between the previous and current malware file execution. HINT:
Use the “stats” command.
• Then save that search as an alert to show a notification when the same type happens
again.


5. Run Splunk >> Forwarder can be in the same system or another system (user’s convenience)
>>Make sure the logs are indexing in the Splunk enterprise.
• Logout of the target system and perform multiple failed attempts. Then use the search
section to filter out the failed attempt logs. Hint: Use the “stats” command.
• Analyze the log file and create an alert for any further similar acti
