# 🛡️ Firewall & DMZ Lab

## 📝 Description
This lab builds upon the previous Active Directory project by deploying an OPNsense firewall for network perimeter security and implementing a segmented DMZ to isolate a web server from the internal network.

## 🛠️ Environment & Tools
* **Hypervisor:** VMware Workstation Pro
* **Firewall:** OPNsense 26.7
* **Operating Systems:** Windows Server 2022 (`DC01`, `WEBSERVER01`), Windows 11 Enterprise (`CLIENT01`)
* **Core Technologies:**
  * Internet Information Services (IIS) Web Server
  * DNS Manager (Forwarders)

## 🌐 Network Overview
| Component | IP Address | Role |
|---|---|---|
| OPNsense WAN | `192.168.68.56` | WAN |
| OPNsense LAN1 | `192.168.64.1` | Internal LAN Gateway |
| DC01 | `192.168.64.128` | DC / DNS / DHCP |
| CLIENT01 | DHCP | LAN1 Client |
| OPNsense LAN2 | `192.168.65.1` | DMZ Gateway |
| WEBSERVER01 | `192.168.65.10` | DMZ Web Server |

## 🚀 Lab Walk-through

### 🔹 Phase 1: Initial Firewall Deployment & Configuration
1. Installed Windows Server 2022 on a virtual machine named `DC01`. *(Figure 1.1)*

2. Configured a permanent static IPv4 address on the server. *(Figure 1.2)*

<br>

<details>
 <summary>📸 Click to view Phase 1 Screenshots</summary>
  <br>
  <p align="center">
   <img width="602" height="155" alt="VM_systeminfo" src="https://github.com/user-attachments/assets/c4ba08e6-bb30-4b47-ab76-cd633450de8f" />
   <br>
   <b>Figure 1.1</b>
   <br><br>
   <img width="397" height="451" alt="DNS_config_after" src="https://github.com/user-attachments/assets/977262a1-b54f-4462-a4b4-bbc3720e70cf" />
   <br>
   <b>Figure 1.2</b>
   <br><br>
</p>
</details>

<br>

### 🔹 Phase 2: Firewall Object Creation & DNS Filtering
1. Installed Windows Server 2022 on a virtual machine named `DC01`. *(Figure 1.1)*

2. Configured a permanent static IPv4 address on the server. *(Figure 1.2)*

<br>

<details>
 <summary>📸 Click to view Phase 2 Screenshots</summary>
  <br>
  <p align="center">
   <img width="602" height="155" alt="VM_systeminfo" src="https://github.com/user-attachments/assets/c4ba08e6-bb30-4b47-ab76-cd633450de8f" />
   <br>
   <b>Figure 2.1</b>
   <br><br>
   <img width="397" height="451" alt="DNS_config_after" src="https://github.com/user-attachments/assets/977262a1-b54f-4462-a4b4-bbc3720e70cf" />
   <br>
   <b>Figure 2.2</b>
   <br><br>
</p>
</details>

<br>

### 🔹 Phase 3: LAN1 Traffic Access Control Configuration
1. Installed Windows Server 2022 on a virtual machine named `DC01`. *(Figure 1.1)*

2. Configured a permanent static IPv4 address on the server. *(Figure 1.2)*

<br>

<details>
 <summary>📸 Click to view Phase 3 Screenshots</summary>
  <br>
  <p align="center">
   <img width="602" height="155" alt="VM_systeminfo" src="https://github.com/user-attachments/assets/c4ba08e6-bb30-4b47-ab76-cd633450de8f" />
   <br>
   <b>Figure 3.1</b>
   <br><br>
   <img width="397" height="451" alt="DNS_config_after" src="https://github.com/user-attachments/assets/977262a1-b54f-4462-a4b4-bbc3720e70cf" />
   <br>
   <b>Figure 3.2</b>
   <br><br>
</p>
</details>

<br>

### 🔹 Phase 4: LAN2 Traffic Access Control & DMZ Deployment
1. Installed Windows Server 2022 on a virtual machine named `DC01`. *(Figure 1.1)*

2. Configured a permanent static IPv4 address on the server. *(Figure 1.2)*

<br>

<details>
 <summary>📸 Click to view Phase 4 Screenshots</summary>
  <br>
  <p align="center">
   <img width="602" height="155" alt="VM_systeminfo" src="https://github.com/user-attachments/assets/c4ba08e6-bb30-4b47-ab76-cd633450de8f" />
   <br>
   <b>Figure 4.1</b>
   <br><br>
   <img width="397" height="451" alt="DNS_config_after" src="https://github.com/user-attachments/assets/977262a1-b54f-4462-a4b4-bbc3720e70cf" />
   <br>
   <b>Figure 4.2</b>
   <br><br>
</p>
</details>

<br>
