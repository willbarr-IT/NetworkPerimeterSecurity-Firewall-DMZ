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
| OPNsense LAN1 | `192.168.64.1/24` | Internal LAN Gateway |
| DC01 | `192.168.64.128` | DC / DNS / DHCP |
| CLIENT01 | DHCP | LAN1 Client |
| OPNsense LAN2 | `192.168.65.1/24` | DMZ Gateway |
| WEBSERVER01 | `192.168.65.10` | DMZ Web Server |

## 🚀 Lab Walk-through

### 🔹 Phase 1: Initial Firewall Deployment & Configuration
1. Deployed a three-interface firewall on a virtual machine and created a strong new password in the OPNsense UI. *(Figure 1.1 & Figure 1.2)*

2. Assigned IPs to the two LAN interfaces with `LAN1` as `192.168.64.1` and `LAN2` as `192.168.65.1`. *(Figure 1.3)*

3. Configured network adapter settings on `DC01` with the OPNsense `LAN1` address as the default gateway and DNS forwarder. *(Figure 1.4 & Figure 1.5)*

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
1. Created a `Microsoft_Updates` alias containing verified Microsoft domains used for client updates within the OPNsense web GUI. Verified the alias populated with the corresponding IP addresses for the configured domains. *(Figure 2.1 & Figure 2.2)*

2. Created a `Web_Ports` alias containing both port `80` (HTTP) and `443` (HTTPS) for ease of use in later configuration of firewall rules. *(Figure 2.3)*

3. Configured Quad9's public DNS servers (`9.9.9.9` and `149.112.112.112`) as the upstream DNS servers to provide security-focused name resolution and ensured that query forwarding was enabled in Unbound's DNS settings. *(Figure 2.4 & Figure 2.5)*

4. Added and enabled HaGeZi's PRO++, Threat Intelligence Feeds, and DoH/VPN/TOR/Proxy Bypass blocklists to provide enhanced protection against malicious domains while preventing users from bypassing local network policy. *(Figure 2.6)* 

5. Configured DNAT (Destination Network Address Translation) rules redirecting any non-local DNS queries originating from the `LAN1` and `LAN2` network back to the firewall's local DNS resolver to further enforce DNS filtering. *(Figure 2.7)*

6. Verified the DNAT rule and blocklists by executing `nslookup` on the blocked domain `doubleclick.net` through Google's public DNS server (`8.8.8.8`). The query returned `0.0.0.0`, demonstrating that the request was intercepted and blocked by the firewall. *(Figure 2.8)*

<br>

<details>
 <summary>📸 Click to view Phase 2 Screenshots</summary>
  <br>
  <p align="center">
  <img width="1000" height="740" alt="MS_Updates_Aliases" src="https://github.com/user-attachments/assets/25b9b702-4ec7-4dba-99df-1ffdf0bf8239" />
   <br>
   <b>Figure 2.1</b>
   <br><br>
  <img width="477" height="810" alt="FW_Diagnostics_MSupdates" src="https://github.com/user-attachments/assets/74fa400e-2de8-41f3-a1ac-430f8a9b9060" />
   <br>
   <b>Figure 2.2</b>
   <br><br>
  <img width="866" height="621" alt="Web_Ports_Aliases" src="https://github.com/user-attachments/assets/9769aecd-85fd-41ba-be6f-f24199434407" />
   <br>
   <b>Figure 2.3</b>
   <br><br>
  <img width="1028" height="887" alt="upstream-dns" src="https://github.com/user-attachments/assets/12d1caea-ca1e-43c0-b96f-08adb670f8b0" />
   <br>
   <b>Figure 2.4</b>
   <br><br>
 <img width="635" height="337" alt="dns-query-forwarding" src="https://github.com/user-attachments/assets/7ce034f4-dba1-456a-9e57-4c831af36af4" />
   <br>
   <b>Figure 2.5</b>
   <br><br>
 <img width="1466" height="492" alt="Blocklists" src="https://github.com/user-attachments/assets/c7a12cc0-c7c2-46ce-ad81-b1d4d4b5cf3a" />
   <br>
   <b>Figure 2.6</b>
   <br><br>
 <img width="1893" height="405" alt="LAN2-DNS-redirect" src="https://github.com/user-attachments/assets/fa84f6f5-4818-4419-952a-3a38ee8d2589" />
   <br>
   <b>Figure 2.7</b>
   <br><br>
  <img width="558" height="320" alt="Hagezi_tests" src="https://github.com/user-attachments/assets/6e45ad23-1fc6-41ff-943c-a053ab2d860a" />
   <br>
   <b>Figure 2.8</b>
   <br><br>
</p>
</details>

<br>

### 🔹 Phase 3: LAN1 Traffic Access Control
1. **DNS access:** Configured a rule allowing DNS traffic (TCP/UDP port `53`) from `LAN1 net` to the firewall's `LAN1 address`, permitting clients to use OPNsense for filtered DNS resolution. *(Figure 3.1)*

2. **Microsoft access:** Configured a rule allowing TCP/UDP traffic from `LAN1 net` to the `Microsoft_Updates` alias over the `Web_Ports` alias (`80`/`443`), permitting Microsoft traffic required for client updates while restricting general internet access. *(Figure 3.1)*

3. **Ping access:** Configured a rule allowing ICMP traffic from `LAN1 net` to the firewall's `LAN1 address`, permitting connectivity testing and troubleshooting. *(Figure 3.1)*

4. **Default deny:** Configured a final explicit deny rule to block all remaining traffic originating from `LAN1 net`. *(Figure 3.1)*

5. **Verified allowed traffic:** Used PowerShell `Test-NetConnection` to verify that a whitelisted Microsoft domain was accessible over the configured web ports. *(Figure 3.2)*

>[!NOTE]
> I originally tried to verify access to the Microsoft domain through a web browser; however, the page did not load. Upon troubleshooting the issue, I found that Microsoft pages load additional dependencies that were not explicitly included in my `Microsoft_Updates` whitelist, resulting in the page failing to load. Therefore, I used PowerShell's `Test-NetConnection` command to verify that a direct TCP connection to the domain could be established.

6. **Verified blocked traffic:** Attempted to access `facebook.com` from the `LAN1` client, confirming that traffic outside the permitted rules was blocked. *(Figure 3.3)*

<br>

<details>
 <summary>📸 Click to view Phase 3 Screenshots</summary>
  <br>
  <p align="center">
    <img width="1615" height="793" alt="LAN1_FW_Rules" src="https://github.com/user-attachments/assets/60dcc0ec-6436-4c3e-bdfa-3618ab6df185" />
   <br>
   <b>Figure 3.1</b>
   <br><br>
   <img width="827" height="187" alt="Whitelisted_Domains_verify" src="https://github.com/user-attachments/assets/4d7f8cf4-c1fe-4ba0-a199-955adcff4385" />
   <br>
   <b>Figure 3.2</b>
   <br><br>
    <img width="917" height="917" alt="Implicit-Deny_verify" src="https://github.com/user-attachments/assets/59a8555d-9d37-4510-a452-aa3eada1d0ae" />
   <br>
   <b>Figure 3.3</b>
   <br><br>
</p>
</details>

<br>

### 🔹 Phase 4: LAN2 Traffic Access Control & DMZ Deployment
1. Deployed the IIS Web Server role on `WEBSERVER01`, a Windows Server 2022 VM, and configured its network adapter to use the OPNsense `LAN2` interface (`192.168.65.1`) as both the default gateway and DNS server. *(Figure 4.1)*

2. Created a custom HTML page displaying **"Welcome to the isolated DMZ web server!"** and configured IIS to prioritize the page by moving the HTML file to the top of the Default Document list. *(Figure 4.2 & Figure 4.3)*

3. **LAN2 DNS access:** Configured a rule allowing DNS traffic (TCP/UDP port `53`) from `LAN2 net` to the firewall's `LAN2 address`, permitting the web server to use OPNsense for filtered DNS resolution. *(Figure 4.4)*

4. **LAN2 internet access:** Configured a temporary maintenance rule allowing traffic from `LAN2 net` to the internet over the `Web_Ports` alias (`80`/`443`) to permit necessary web-based updates. The rule remained disabled until needed to maintain DMZ restrictions. *(Figure 4.4)*

5. **LAN2-to-LAN1 isolation:** Configured a rule blocking all traffic from `LAN2 net` to `LAN1 net`, preventing the DMZ web server from initiating any connections to the internal LAN. *(Figure 4.4)*

6. **Verified DMZ isolation:** Verified the LAN2-to-LAN1 restriction through firewall logs, which showed ping attempts from the DMZ being blocked. *(Figure 4.5)*

7. **Published DMZ web server:** Configured a DNAT port forwarding rule on the `WAN` interface to redirect incoming HTTP traffic to `WEBSERVER01` on the DMZ network, allowing external access to the webpage. *(Figure 4.6)*

8. **Verified external access:** Accessed the DMZ web server from the host PC using the OPNsense `WAN` address, successfully displaying the custom IIS webpage. *(Figure 4.7)*

<br>

<details>
 <summary>📸 Click to view Phase 4 Screenshots</summary>
  <br>
  <p align="center">
  <img width="462" height="554" alt="webserver-dns-settings" src="https://github.com/user-attachments/assets/bdfca2e2-9209-4d0b-b1f5-efe60731f9f6" />
   <br>
   <b>Figure 4.1</b>
   <br><br>
  <img width="975" height="414" alt="html-doc" src="https://github.com/user-attachments/assets/26c9d413-db14-49f9-b7c4-f9b9db7e9349" />
   <br>
   <b>Figure 4.2</b>
   <br><br>
   <img width="709" height="587" alt="moving-index-file-top" src="https://github.com/user-attachments/assets/c080d4ef-9fe9-4c6c-b249-f9f3de08186c" />
   <br>
   <b>Figure 4.3</b>
   <br><br>
   <img width="1863" height="514" alt="LAN2FWrules" src="https://github.com/user-attachments/assets/5cc6b0fd-21ea-4b78-9c4a-4680d7fbcf58" />
   <br>
   <b>Figure 4.4</b>
   <br><br>
   <img width="2006" height="180" alt="LAN2-Isolation-Check-Log" src="https://github.com/user-attachments/assets/52b53dd0-7c58-41a5-814e-af36803a1422" />
   <br>
   <b>Figure 4.5</b>
   <br><br>
  <img width="1893" height="471" alt="externall-access-dmz" src="https://github.com/user-attachments/assets/3c4fc79e-4682-48e2-be2f-b1388db8cd66" />
   <br>
   <b>Figure 4.6</b>
   <br><br>
     <img width="1149" height="397" alt="HostPc-DMZ" src="https://github.com/user-attachments/assets/1ebdebd0-52ec-4fac-94fc-56f1bb096ce1" />
   <br>
   <b>Figure 4.7</b>
   <br><br>
</p>
</details>

<br>
