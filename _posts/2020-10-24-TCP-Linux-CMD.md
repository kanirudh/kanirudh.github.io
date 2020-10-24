---
layout: post
title: TCP Command Line Tools on Linux
---

For any decent systems programmer on Linux, there will be time when he has to debug a pcap file.
No understanding the nuances of TCP/IP are for another topic but here we just want to get started
with opening and investigatin those pcap files.

## tshark

It is such an awesome tool, to read the pcap file on command line. And I find its faster than wireshark
as well. Since, the underlying library is libpcap, there is not difference in terms of features.

### Read a summary of the file
    tshark -r <pcap_file>

### Print the each packet in excrutiating detail
    tshark -Vx -r <pcap_file>

### Apply some filters
    tshark -r <pcap_file> "filters"

Lets say you want to filter on the frame number
    tshark -Vx -r <pcap_file> "frame.number == 1"

Filter based on the ip, port
    tshark -r <pcap_file> "ip.addr == 10.168.87.69 && tcp.port == 30003"

### Enable absolute timestamps
    tshark -t a -r <pcap_file>

### Enable/Disable TCP Relative sequence numbers
    tshark -o -o tcp.relative_sequence_numbers:FALSE -r <pcap_file>

## tcpwrite

Sometimes, we want to use the payload data from some older communication and modify the ip.
Following commands, can do help do the same easily

    tcpprep -a client -i packets_20201001.44.solarcapture.pcap -o cache_20201001

    tcprewrite --cachefile=cache --endpoints=192.168.35.11:192.168.35.10 -i packets_20201022.52.solarcapture.pcap -o edited.pcap


