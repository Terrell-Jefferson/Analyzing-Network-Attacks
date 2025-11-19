# Analyzing-Network-Attacks

# Table of contents

1. [Introduction](#introduction)
2. [Scenario](#scenario)
3. [Cybersecurity Incident Report](#cybersecurity-incident-report)

-------

# Introduction <a name="introduction">

A mock analysis of a DoS network attack for an affected company, completed as part of my cybersecurity portfolio and as part of Google's <a href='https://www.coursera.org/google-certificates/cybersecurity-certificate'>Cybersecurity Professional Certificate</a> on Coursera in the  <a href='https://www.coursera.org/learn/networks-and-network-security/home'> Connect and Protect: Networks and Network Security </a> Course .
   
The goal is to investigate a critical service interruption by analyzing abnormal TCP traffic captured from a packet sniffer. The objective is to identify the type of attack affecting the organization’s web server, interpret patterns such as excessive SYN requests, and determine how the attack caused connection timeouts for employees and customers. This exercise requires reviewing packet-level evidence, documenting findings, identifying the likely attack method, and communicating the impact and next steps to management.

# Scenario  <a name="scenario">
You work as a security analyst for a travel agency that advertises sales and promotions on the company’s website. The employees of the company regularly access the company’s sales webpage to search for vacation packages their customers might like. 

One afternoon, you receive an automated alert from your monitoring system indicating a problem with the web server. You attempt to visit the company’s website, but you receive a connection timeout error message in your browser.

You use a packet sniffer to capture data packets in transit to and from the web server. You notice a large number of TCP SYN requests coming from an unfamiliar IP address. The web server appears to be overwhelmed by the volume of incoming traffic and is losing its ability to respond to the abnormally large number of SYN requests. You suspect the server is under attack by a malicious actor. 

You take the server offline temporarily so that the machine can recover and return to a normal operating status. You also configure the company’s firewall to block the IP address that was sending the abnormal number of SYN requests. You know that your IP blocking solution won’t last long, as an attacker can spoof other IP addresses to get around this block. You need to alert your manager about this problem quickly and discuss the next steps to stop this attacker and prevent this problem from happening again. You will need to be prepared to tell your boss about the type of attack you discovered and how it was affecting the web server and employees.

[Wireshark TCP_HTTP log.xlsx](https://github.com/user-attachments/files/23618289/Wireshark.TCP_HTTP.log.xlsx) (**OPEN IN GOOGLE SHEETS**)


# Cybersecurity Incident Report  <a name="cybersecurity-incident-report">

Section 1: Identify the type of attack that may have caused this
network interruption

**One potential explanation for the website's connection timeout error message is:** A denial-of-service (DoS) attack.

**The logs show that:** A large number of TCP SYN packets were sent from an unfamiliar IP address, overwhelming the server and preventing it from completing connection requests.

**This event could be:** A SYN flood attack, which is a specific type of DoS attack that overwhelms a server by flooding it with incomplete TCP handshakes.

-------

Section 2: Explain how the attack is causing the website to malfunction

**When website visitors try to establish a connection with the web server, a three-way
handshake occurs using the TCP protocol. Explain the three steps of the handshake:**

1. SYN: The client sends a SYN packet to the server to request a connection.

2. SYN-ACK: The server responds with a SYN-ACK packet, meaning it acknowledges the client's request and is also ready to connect.

3. ACK: The client sends a final ACK packet to acknowledge the connection and complete the setup.


**Explain what happens when a malicious actor sends a large number of SYN packets all at
once:** The server allocates connection slots and resources for each SYN it receives, but the attacker never completes the handshake with an ACK. Thus, the server fills up its queue of half-open connections due to multiple SYN packets being received, and there is no space/available resources for anyone else.

**Explain what the logs indicate and how that affects the server:** The logs show a flood of SYN packets from a suspicious IP address (203.0.113.0). This affects the server’s connection queue by overwhelming it, causing it to stop responding to normal requests. In the end, the server is too overwhelmed and can no longer establish complete TCP sessions.

-------

