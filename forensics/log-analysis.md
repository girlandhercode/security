# Log Analysis



**Find how many different IP addresses in the log**

```text
cat squid_access.log | awk '{print $3}' | sort | uniq -c
```

**Fun with apache logs**

[https://www.the-art-of-web.com/system/logs/](https://www.the-art-of-web.com/system/logs/)

**To pull out everything but text \(always better to filter by what you don't want to ensure you don't accidentally exclude**

```text
grep -v "text"
```

**To pull out IP addresses**

```text
grep -Po "[0-9]+\.[0-9]+\.[0-9]+\.[0-9]+"
```

**Sort and find unique occurrences**

```text
| sort | uniq -c
```

**Count number of lines**

```text
wc -l
```

**Basic wireless PCAP analysis**

```text
wireshark 
or
aircrack-ng <filename>
```

Sometime aircrack-ng can find the WEP password. If so the you can use the password in wireshark to decrypt the traffic

```text
This can be done by selecting “Edit > Preferences > Protocols > IEEE 802.11” and
then checking “Enable decryption” and adding the decryption key.
```

To discover the wireless network name, aircrack has a wordlist function

```text
aircrack-ng PCAP.cap -w /usr/share/wordlists/rockyou.txt
```

