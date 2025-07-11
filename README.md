🛡️ Suricata + Wireshark: ICMP Traffic Detection & Analysis

📘 Overview

This project demonstrates the configuration and deployment of **Suricata** as a Network Intrusion Detection System (IDS) on **Kali Linux**, alongside **Wireshark** for live packet capture and traffic analysis.

By crafting and testing custom detection rules, the lab focuses on identifying **ICMP Echo Requests** (ping traffic) and analyzing them in detail to simulate a real-world SOC (Security Operations Center) workflow.

🔧 Tools Used
- Kali Linux (VirtualBox Bridged Adapter)
- Suricata IDS
- Wireshark
- ICMP traffic simulation via `ping`

📌 Key Objectives
- Install and configure Suricata as IDS
- Write custom alert rule for ICMP ping requests
- Update and apply Suricata rule sets
- Capture and analyze ICMP traffic with Wireshark
- Validate alert generation through Suricata logs

🚀 Setup Instructions

1. **Install Suricata**  
   ```bash
   sudo apt update && sudo apt install suricata
   ```

2. **Update Rule Sets**  
   ```bash
   sudo suricata-update
   ```

3. **Create Custom Rule**  
   File: `/var/lib/suricata/rules/local.rules`  
   ```plaintext
   alert icmp any any -> any any (msg:"ICMP Ping Detected"; itype:8; sid:1000001; rev:1;)
   ```

4. **Configure suricata.yaml**  
   Include `local.rules` in `rule-files` section and verify `default-rule-path`.

5. **Restart Suricata**  
   ```bash
   sudo systemctl restart suricata
   ```

6. **Test Rule**  
   Generate ICMP traffic:  
   ```bash
   ping -c 4 8.8.8.8
   ```

7. **Verify Detection**  
   ```bash
   sudo cat /var/log/suricata/eve.json | grep "ICMP Ping Detected"
   ```

## 🔍 Packet Analysis with Wireshark

- Capture live traffic on the active interface
- Filter for ICMP traffic using:
  ```
  icmp
  ```
- Examine details such as type (Echo Request/Reply), TTL, IP headers, and payload structure

## ✅ Outcome

Successfully detected and logged ICMP ping activity using Suricata and verified traffic structure and flow with Wireshark. This reinforces hands-on IDS rule creation, traffic inspection, and packet-level analysis—vital for blue team practitioners.

## 📁 Author

Joshua | Cybersecurity Learner & SOC+ Lab Explorer  
📌 Focused on blue team skills, threat detection, and network security labs.
