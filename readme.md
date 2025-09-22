Nmap Project – Basic Network Reconnaissance

Objective
         Perform a basic network reconnaissance of my local network using Nmap to identify open ports and      	services, then document potential security risks.


						Steps Performed
						
	1. Installed Nmap** on Linux from the official repository.
	2. Found local IP range using:
 					  ip a

	Identified host IP: 10.0.2.2/24 → network range: 10.0.2.0/24.
	3. Scanned the network:
			nmap -sS 10.0.2.0/24 -oN reports/scan.txt

	4. Saved results in reports/scan.txt.

	5. Captured key screenshots and stored them in the screenshots/ folder.

	6. Analyzed open ports and their services, noting potential security implications.

| IP Address | Open Ports | Services            | Observations / Risks                                                                  |
| ---------- | ---------- | ------------------- | ------------------------------------------------------------------------------------- |
| 10.0.2.2   | 135, 445   | MSRPC, Microsoft-DS | Windows RPC & file sharing; fine on LAN but must be firewalled from the internet.     |
| 10.0.2.2   | 3306       | MySQL               | Database service; must use strong credentials and avoid external exposure.            |
| 10.0.2.2   | 4343       | Unicall             | Custom/unknown service; restrict access to trusted devices only.                      |
| 10.0.2.2   | 4449       | PrivateWare         | Private/custom service; unknown security implications, monitor or firewall as needed. |


						Conclusion

	The scan revealed multiple open ports on host 10.0.2.2.
	Standard services like MSRPC, Microsoft-DS, and MySQL can be exploited if exposed externally.
	Custom services such as Unicall and PrivateWare should be monitored closely and access limited.
	This task strengthened my understanding of:

	Port scanning and service detection
	Network reconnaissance
	The importance of proper firewall rules and hardening

___________________________________________________________________________________________________________________________________________________________________
___________________________________________________________________________________________________________________________________________________________________
															  ## Wireshark Capture & Analysis

Capture Details
- Host captured: 10.0.2.15
- Capture file: captures/session1.pcapng
- Capture duration: ~5 seconds (adjust based on your capture)
- Total packets: 32 (adjust based on your capture)

 Filters Used
- `ip.addr == 10.0.2.15` → focus on traffic to/from our host
- `tcp.flags.syn == 1 && tcp.flags.ack == 0` → highlight Nmap TCP SYN scan packets
- `tcp.port == 3306` → MySQL traffic (optional)
- `dns` → DNS queries

 Key Observations
1. **DNS Queries**
   - Host 10.0.2.15 queried DNS server 192.168.1.254 for `play.picoctf.org`
   - Responses returned A and AAAA records

2. **QUIC Traffic**
   - Host performed QUIC handshake with 172.66.157.191
   - Handshake packets exchanged (Initial, Handshake, Protected Payload)
   - Encrypted application data observed after handshake

3. **TLS / HTTPS Traffic**
   - Encrypted communication established with servers:
     - 34.107.243.93 (TLSv1.2)
     - 151.101.129.91 (TLSv1.2)
   - TCP ACK packets confirm reliable delivery

4. **Nmap TCP SYN Packets**
   - SYN packets sent to open ports discovered in Nmap scan (135, 445, 3306, 4343, 4449)
   - Host responded with SYN-ACK or RST
   - Confirms which services are active and reachable




w

  
