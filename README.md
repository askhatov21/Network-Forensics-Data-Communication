# Network-Forensics-Data-Communication
# Student: Askhatov Amir
# Course: CP2409 – Data Communications & Networks

📋 Project Overview
This assignment is a network forensics and performance analysis of the fictional company BoredGames, which reported consistently slow application loading, slow file transfers to the internal file server, and sluggish internet browsing. The analysis uses real packet capture data (A1_Bad_Packets.pcapng) examined through Wireshark to identify root causes using the OSI model as a troubleshooting framework.


📁 Repository structure: 
CP2409_Assignment_1.pdf # Full written report

A1_Bad_Packets.pcapng # Wireshark capture packet


🔍 Tools Used
ToolPurposeWiresharkPrimary packet capture and analysis toolWireshark Expert InfoDetected TCP warnings (Zero Window, RST, out-of-order)Wireshark I/O GraphsVisualised error bursts and throughput over timeWireshark ConversationsIdentified single TCP stream between 10.0.52.164 ↔ 61.8.0.17Protocol HierarchyConfirmed TCP/IPv4 dominance; minimal HTTP traffic


🧱 OSI Layer Analysis Summary
LayerIssue FoundL1 – PhysicalSuspected cabling issues causing bit errors and retransmissionsL2 – Data LinkPossible duplex mismatch (full vs half-duplex) causing collisionsL3 – NetworkLatency spikes and packet reordering; 6 MB took 125 secondsL4 – TransportPrimary issue: TCP retransmissions, duplicate ACKs, Zero Window, RST eventsL5 – SessionUnstable sessions due to repeated resets mid-transferL6 – PresentationMinimal TLS overhead; only 1 HTTP packet capturedL7 – ApplicationSMB/FTP slowness; DNS resolution latency suspected

📊 Key Findings from Wireshark

Throughput: ~0.35 Mbps on a gigabit-capable link — severely underutilised
Packet count: 7,195 packets; 6 MB transferred over 125 seconds
Expert Info Warnings:

TCP Zero Window – receiver buffer full, sender forced to pause
TCP Window Full – application not reading buffer fast enough
Connection Reset (RST) – sessions abruptly terminated
Out-of-Order Segments – packets arriving out of sequence


Error bursts: Concentrated at 0–25s and 50–100s intervals (visible in I/O Graph)


🛠️ Recommendations
Immediate (within 7 days)

Verify NIC and switch are both set to 1 Gbps full-duplex
Replace patch cables and test for CRC errors
Ensure consistent MTU of 1500 across all devices
Check DNS resolver response times and caching

Short-Term (1–4 weeks)

Enable TCP window scaling for high-latency paths
Implement QoS policies to prioritise SMB and HTTP control traffic
Monitor with SNMP for interface errors and buffer utilisation

Long-Term (1–3 months)

Deploy managed switches with flow control support
Introduce performance dashboards tracking retransmission %, zero-window events, and RTT
Consider Software-Defined Networking (SDN) for dynamic traffic rerouting


📄 References
Key references used in this analysis:

Wireshark Foundation, Wireshark User's Guide: TCP Analysis, v4.2, 2024
Cisco Systems, Troubleshooting Duplex and Speed Mismatches, TAC White Paper, 2023
RFC 793 (TCP), RFC 7323 (TCP Extensions for High Performance)
Microsoft, SMB Performance Optimization Guidelines, 2022
Kurose & Ross, Computer Networking: A Top-Down Approach, 8th ed., Pearson, 2021



📄 License
All work in this repository is submitted as academic coursework at James Cook University. Not for redistribution.
