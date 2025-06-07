# Ph4nt0m 1ntrud3r

## Category - Forensics

### Challenge Description

A digital ghost has breached my defenses, and my sensitive data has been stolen! 😱💻 Your mission is to uncover how this phantom intruder infiltrated my system and retrieve the hidden flag.
To solve this challenge, you'll need to analyze the provided PCAP file and track down the attack method. The attacker has cleverly concealed his moves in well timely manner. Dive into the network traffic, apply the right filters and show off your forensic prowess and unmask the digital intruder!
Find the PCAP file here Network Traffic PCAP file and try to get the flag.

### Hints

1. Filter your packets to narrow down your search. 
2. Attacks were done in timely manner. 
3. Time is essential

### Solution

I opened the pcap file in Wireshark to test for anomalies and to see if there's something useful out of it, I came across multiple "===" signs in various packets which upon searching I found out that
they represent base 64 encoding, Then it was pretty much not difficult from there as i just sorted all the packets which had "===" with "time" as their filter and just decoded the texts in that order 
and I was able to obtain the flag.



Hence solved xd
