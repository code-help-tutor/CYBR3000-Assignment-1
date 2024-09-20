# CYBR3000 Information Security Assignment

## Introduction
This assignment is divided into two parts: Part A and Part B.

### Part A: Intrusion Prevention (25 marks total)
- You are required to write `iptables` rule sets for each of the following tasks. Each rule set for each of the tasks needs to be written in a separate `.txt` file. Each line in the `.txt` file refers to one single `iptables` rule. The name of the `.txt` file must match the name of the corresponding task (e.g. `task1.txt`). No marks will be given if the name of the `.txt` file is incorrect or mislabelled. The rules in each `.txt` file are supposed to be ready to use, which means others could copy-paste and run each rule of the rule set in the terminal to meet the requirements of the task.
- To use `iptables`, you need to test your rules in a Linux-based system. Tools like Docker or a VM using software like VirtualBox or VMware would allow you to run a Linux environment where `iptables` can be used.

Tasks:
- **Task 1 (5 marks)**: Allow incoming SSH traffic (which is using port 22) from a specific IP address (192.168.1.100) and deny all other incoming SSH connections.
- **Task 2 (5 marks)**: Allow incoming HTTP (port 80) and HTTPS (port 443) traffic but drop all other incoming traffic.
- **Task 3 (5 marks)**: Limit incoming ICMP ping requests (ICMP echo-request) to only two per second.
- **Task 4 (5 marks)**: Allow only established and related connections for incoming traffic, blocking new incoming connections except for SSH.
- **Task 5 (5 marks)**: Block all incoming and outgoing traffic by default but allow SSH access from a specific IP (192.168.1.100), HTTP/HTTPS traffic, and DNS queries.

### Part B: Intrusion Detection (75 marks in total)
- In this part, you are required to write a Python program called `IDS.py` that mimics the behaviour of an Intrusion Detection System (IDS). This program would read two files: 1) one file includes intrusion detection rules (like rules used in Snort) and 2) the other file is the `.pcap` file that contains all the packets that your program would go through to check if any or some of them violates the rules. Both files will be passed into your Python program (IDS.py) through the Command-Line Argument. The start of `IDS.py` would be:
```
$python3 NIDS.py <path_to_the_pcap_file> <path_to_the_IDS_rules>
```
Both paths need to be absolute paths.
- Python 3.9 is the version required for this part and the final test for marking this assignment will use Python 3.9 as well. We will not allow the use of any other Python versions, and no marks will be given if unexpected behaviours happen due to the wrong Python version. Scapy is the library allowed in this part, do not use any other external library in your code.
- Examples for both `IDS_rules.txt` and `.pcap` files are given on the BlackBoard. You need to read and parse each rule and use the rule to monitor and detect packets in the `.pcap` file. Please be aware that the provided `.pcap` files are only a subset of the `.pcap` file which will be used in the final marking of this assignment.
- The format of the IDS rules is like the format of snort rules with slight differences. One simple example of your IDS rules is:
```
alert tcp 192.168.102.132 any -> any any (msg: "receive a TCP packet";)
```
This rule would raise an alert when the packet is an incoming TCP packet that comes from any port from IP address 192.168.102.132 and is sent to any port number in any IP address. If a packet like that is found, the `IDS.py` would log the message into a log called `IDS_log.txt` that has the following format:
```
2024 - 08 - 18 11:47:53 - Alert: receive a TCP packet
2024 - 08 - 18 11:47:53 - Alert: receive a TCP packet
... (if more packets are found)
```
Each line in the `IDS_log.txt` represents that the IDS finds a packet that meets at least one of the rules. Each line starts with a time stamp and then follows with `Alert: <content_in_msg>`. The `IDS_log.txt` must match the format given above since you will be marked based on this.
- A more complicated example is:
```
alert tcp 192.168.102.132 any -> 131.171.127.1 25 (content: "malicious"; msg: "multiple malicious TCP syn packets found"; flags: S; detection_filter: count 10, seconds 2;)
```
In this example, the `IDS.py` would raise an alert if the IDS found more than 10 TCP syn packets within 2 seconds is sent from any port number from IP address 192.168.102.132 to port 25 on IP address 131.171.127.1 that has a content that contains string “malicious”.
- Your `IDS.py` should ignore any line that starts with “#” in the rule set.

Clarifications:
- The `IDS.py` only has `alert` as the action after detecting a packet.
- The `IDS.py` supports four different protocols: `ip`, `icmp`, `tcp`, `udp`.
- The `IDS.py` does not support IP range, all test cases will have one source IP address and one Destination IP address.
- The `IDS.py` only considers incoming traffic, the “->” symbol would remain the same across all test cases.
- Each rule option inside the brackets in the rule should be separated by “;”. The last option in the rule should finish with a “;” follows with a “)”.
- The “flags” option supports four different types: `A`, `S`, `F`, `R`
    - `A`: ACK (Acknowledgement)
    - `S`: SYN (Synchronize sequence numbers)
    - `F`: FIN (Finish)
    - `R`: RST (Reset the connection)
- “detection_filter” would only and always have two options: “count <the number of packets>”, and “seconds <the time window in second>”. Please follow the exact format provided in the example.

Your `IDS.py` will be tested in the following scenarios (Tasks):
- Detect multiple TCP packets (5 marks).
- Detect multiple ICMP packets (5 marks).
- Detect multiple IP packets (5 marks).
- Detect multiple UDP packets (5 marks).
- Detect a mix of TCP, ICMP, UDP and IP packets (5 marks).
- Detect one packet with malicious content within all other benign packets (5 marks).
- Detect packets with malicious content across different protocols (5 marks).
- Detect TCP syn packets, fin packets, rst packets and ack packets (10 marks).
- Detect TCP flooding (10 marks).
- Detect TCP syn scan (10 marks).
- Detect multiple TCP ack packets with malicious content within a short period of time (10 marks)
# CYBR3000 Assignment 1

# CS Tutor | 计算机编程辅导 | Code Help | Programming Help

# WeChat: cstutorcs

# Email: tutorcs@163.com

# QQ: 749389476

# 非中介, 直接联系程序员本人
