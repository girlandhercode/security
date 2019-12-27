# Wireshark



So now that you have entered a network and intercepted the traffic it is time to analyze that traffic. That can be with wireshark.

### Useful Information <a id="useful-information"></a>

Statistics--&gt;Conversations

A network conversation is the traffic between two specific endpoints. For example, an IP conversation is all the traffic between two IP addresses. This is usful in identifying unusal points in a packet capture, as well as unusally large conversatoins. Don't forget to look in UDP as well for unusal traffic.

Note: The conversations field can also be limited to display statistics based on display fileters \(see the checkbox at the bottmon of the converations window\).

### 

### Filters <a id="filters"></a>

There are two types of filters that we can use.

1. Capture filter
2. This filters out in the capture process, so that it does not capture what you have not specified.
   1. Display filter
3. This filter just filters what you see. You might have captured 1000 packets, but using the display filter you will only be shown say 100 packets that are relevant to you.

The syntax for the two filters are a bit different.

#### Capture filter <a id="capture-filter"></a>

So if you just start capturing all traffic on a network you are soon going to get stuck with a ton of packets. Too many! So we might need to refine out capture.

Click on the fourth icon from the left. If you hover over it it says `Capture options`

Some useful might be.  
From a specific host and with a specific port:

```text
host 192.168.1.102
port 110
```

#### Display filter <a id="display-filter"></a>

Show only packets used by this IP-address, or to a specific port

```text
ip.addr == 192.168.1.102
tcp.port eq 25
```

#### Other filters <a id="other-filters"></a>

[https://wiki.wireshark.org/DisplayFilters](https://wiki.wireshark.org/DisplayFilters)

#### Automatically resolve ip-addresses <a id="automatically-resolve-ip-addresses"></a>

Easy  
[https://ask.wireshark.org/questions/37680/can-wireshark-automatically-resolve-the-ip-address-into-host-names](https://ask.wireshark.org/questions/37680/can-wireshark-automatically-resolve-the-ip-address-into-host-names)

#### Need to save files out of a capture <a id="need-to-save-files-out-of-a-capture"></a>

```text
Try to use File--> Export Objects-->Protocol

If protocol is not listed (for example FTP) then Follow TCP Stream of file data. 
Filter the conversation so only one side is displayed. (side with data)
Convert to RAW ("show and save data as" option) and save the contents to disk.
```

