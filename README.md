# Cybersecurity Incident Report

<h2>Description</h2>
This cybersecurity incident report outlines a network interruption affecting a website by connection timeout error messages. The analysis suggests a potential attack where numerous requests flood the server simultaneously, creating a situation that is distinct from a Distributed Denial of Service (DDoS) attack, as the source IP remains constant.<br /><br />

Upon closer examination of the logs, a critical event at 3.599628 indicates that an additional request was initiated before the completion of the acknowledgment process, resulting in a flood of requests. This abnormal pattern points towards a deliberate attempt to disrupt the server's functionality, possibly with the intention of rendering it inaccessible.
<br />

<h2>Languages and Utilities Used</h2>

- <b>Packet Sniffing</b>
- <b>VirusTotal</b> 

<h2>Walk-through:</h2>

| Section 1: Identify the type of attack that may have caused this network interruption|
| ---         |
| One potential explanation for the website's connection timeout error message is: There are many requests coming it at one time. It is not a DDoS, as the IP address is the same. <br /><br />The logs show that: At 3.599628, another request came in before the Ack and flooded the server.<br /><br />This event could be: Someone trying to stop a server from working. |

| Section 2: Explain how the attack is causing the website to malfunction|
| ---         |
| When website visitors try to establish a connection with the web server, a three-way handshake occurs using the TCP protocol. Explain the three steps of the handshake:<br/><br/> 1. Syn  <br/>2. Syn, Ack <br/>3. Ack <br/><br/>Explain what happens when a malicious actor sends a large number of SYN packets all at once: The server cannot reach phase 3, and if the issue persists, will fire error messages, not allowing step 2 <br/><br/>Explain what the logs indicate and how that affects the server: The server tries to keep up with the request from the one IP address. The server can respond temporarily but is overwhelmed and displays a “time out” message. <br/><br/>If not resolved, it will make the server unusable and halt any use of the server. Additionally, if not addressed, it could cause issues with stored information. We should remove the IP address from any requests.|
<br/>


<p align="left">

Summary:  <br/>
The website disruption stems from a targeted attack, as opposed to a typical DDoS scenario, where a consistent source IP is bombarding the server with an overwhelming number of requests. The attack disrupts the three-way handshake process during establishing the TCP connection. The malicious actor sends excessive SYN packets instead of progressing through the Syn, Syn/Ack, and Ack phases, preventing the server from completing the handshake.<br/><br />

Logs indicate that the server attempts to respond to the flood of requests from a single IP address, leading to temporary responses. However, the server becomes overwhelmed, resulting in connection timeouts. If left unaddressed, this could render the server entirely unusable and potentially compromise stored information. The recommended mitigation involves removing the identified malicious IP address from further requests to restore standard server functionality and prevent future disruptions.

</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
