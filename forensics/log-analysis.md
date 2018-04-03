# Log Analysis

##### Find how many different IP addresses in the log

```
cat squid_access.log | awk '{print $3}' | sort | uniq -c
```

##### Fun with apache logs

[https://www.the-art-of-web.com/system/logs/](https://www.the-art-of-web.com/system/logs/)

##### 

##### 

##### 

##### 

##### Basic wireless PCAP analysis

```
wireshark 
or
aircrack-ng <filename>
```

Sometime aircrack-ng can find the WEP password. If so the you can use the password in wireshark to decrypt the traffic

```
This can be done by selecting “Edit > Preferences > Protocols > IEEE 802.11” and
then checking “Enable decryption” and adding the decryption key.
```

To discover the wireless network name, aircrack has a wordlist function

```
aircrack-ng PCAP.cap -w /usr/share/wordlists/rockyou.txt
```


