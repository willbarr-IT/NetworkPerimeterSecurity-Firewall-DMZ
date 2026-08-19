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
| OPNsense WAN | DHCP | WAN |
| OPNsense LAN1 | `192.168.64.1` | Internal LAN Gateway |
| DC01 | `192.168.64.128` | DC / DNS / DHCP |
| CLIENT01 | DHCP | LAN1 Client |
| OPNsense LAN2 | `192.168.65.1` | DMZ Gateway |
| WEBSERVER01 | `192.168.65.10` | DMZ Web Server |

## 🚀 Lab Walk-through

### 🔹 Phase 1: Initial Firewall Deployment & Configuration
1. Deployed a three-interface firewall on a virtual machine and created a strong new password in the OPNsense UI. *(Figure 1.1 & Figure 1.2)*

2. Assigned IPs to the two LAN interfaces with LAN1 as `192.168.64.1` and LAN2 as `192.168.65.1`. *(Figure 1.3)*

3. Configured network adapter settings on `DC01` with LAN1 as the default gateway and configured the OPNsense LAN1 address as the DNS forwarder. *(Figure 1.4 & Figure 1.5)*

4. Verified connectivity to the firewall by executing `ping` and `nslookup`. *(Figure 1.6)* 

<br>

<details>
 <summary>📸 Click to view Phase 1 Screenshots</summary>
  <br>
  <p align="center">
 <img width="481" height="327" alt="FW_Server_config" src="https://github.com/user-attachments/assets/4781c855-f54e-44f0-b1df-43ec14326b6b" />
   <br>
   <b>Figure 1.1</b>
   <br><br>
<img width="547" height="248" alt="FW_Password_set" src="https://github.com/user-attachments/assets/84ddbab6-62b2-445d-a4a3-ed2a59e22d1f" />
   <br>
   <b>Figure 1.2</b>
   <br><br>
<img width="480" height="95" alt="FW_Interfaces_config" src="https://github.com/user-attachments/assets/3aa93eca-8e62-4e2d-b51c-6090a3e70611" />
<br>
<b>Figure 1.3</b>
<br><br>
<img width="453" height="450" alt="Assigning_FW-to-DG" src="https://github.com/user-attachments/assets/0c819181-fbcf-439f-b0ed-169c84770d13" />
<br>
<b>Figure 1.4</b>
<br><br>
<img width="862" height="360" alt="dns-forwarder-DCtoFW" src="https://github.com/user-attachments/assets/58a85f11-7ee9-4e4c-a780-ce5feda4986d" />
<br>
<b>Figure 1.5</b>
<br><br>
<img width="526" height="452" alt="Testing-FW-Connectivity" src="https://github.com/user-attachments/assets/a87bf2e5-6e69-42ed-94ed-8edcc15b8add" />
<br>
<b>Figure 1.6</b>
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

### 🔹 Phase 3: LAN1 Traffic Access Control
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
