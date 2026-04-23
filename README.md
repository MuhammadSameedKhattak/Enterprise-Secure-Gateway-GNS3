# 3-Tier Secure Corporate Gateway (GNS3)

## 📌 Project Overview
Designed and deployed a secure enterprise network boundary using Cisco IOS within GNS3. The architecture physically and logically separates traffic into three distinct security zones (Inside, Outside, and DMZ) to protect internal assets while hosting public-facing services.

## 🏗️ Topology & Architecture
![Network Topology](https://github.com/MuhammadSameedKhattak/Enterprise-Secure-Gateway-GNS3/blob/main/GNS3diagram.png?raw=true)
**Network Zones:**
* **Inside (192.168.10.0/24):** Secured employee network.
* **DMZ (172.16.1.0/24):** Public-facing web server zone.
* **Outside (203.0.113.0/24):** Simulated Internet/WAN link.

## ⚙️ Core Technologies Implemented
* **NAT Overload (PAT):** Configured dynamic translation for the `Inside` network, disguising internal employee traffic behind a single public IP address.
* **Stateless Access Control Lists (ACLs):** Engineered strict inbound filtering on the WAN interface to aggressively drop unauthorized ICMP and TCP traffic attempting to reach the internal LAN.
* **Zone-Based Routing:** Verified inter-VLAN routing and DMZ accessibility, ensuring the public can reach the web server without compromising the employee subnet.

## 🛠️ Validation & Troubleshooting
Real-world deployments rarely go perfectly. During this lab, I successfully debugged several system-level infrastructure issues:
1.  **Memory Fragmentation Limitations:** Handled Cisco IOS NBAR engine crashes by tuning emulator RAM allocation to match legacy 32-bit hardware constraints.
2.  **Packet-Level Debugging:** Utilized `debug ip nat` and `debug ip icmp` to track packet flow matrixes, identifying and resolving stateless ACL drops on ICMP return traffic.

## 📊 Proof of Concept
### NAT Translation Matrix
![NAT Proof](https://raw.githubusercontent.com/MuhammadSameedKhattak/Enterprise-Secure-Gateway-GNS3/main/validation/NAT-Matrix.png)
*Caption: Active PAT table confirming successful translation of the Inside Local IP to the Inside Global IP.*

### Firewall ACL Hit Counters
![ACL Proof](https://github.com/MuhammadSameedKhattak/Enterprise-Secure-Gateway-GNS3/blob/main/firewalldenial.png?raw=true)
*Caption: Validation of ACL 100 actively dropping unauthorized external ICMP requests to the internal LAN.*
