# Scapy



Tool for creating packets and packet manipulation

```text
#Scapy..make me a packet
>>>packet=IP(dst="10.10.10.50")/TCP(dport=22)

#Scapy..send my packet, storing the response in a variable called response
>>>response=sr(packet)

#Scapy..look at my response
>>>response

#Scapy..look at first part of the first set of my response
>>>response[0][0]
```

Send packet with a payload

```text
>>>packet=(IP(dst="10.10.10.50")/TCP(dport=22)/"thisisthetestpayload")
```

To make a loop \(overflow\)--once per second

```text
>>>packet=IP(dst="10.10.10.50")/ICMP()
>>>srloop(packet)
```

Get packets from a pcap file

```text
>>>rdpcap("[filename]",[packets])
```

