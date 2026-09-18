# Network Reconnaissance & Subnet Discovery Operations

## Project Overview
This repository details the execution of two foundational cybersecurity operational phases: **Passive Footprinting & Reconnaissance** using Kali Linux CLI utilities[cite: 6, 7, 8, 9, 10, 11, 12] and **Active Subnet Discovery** using Zenmap[cite: 3, 4, 5]. The objective was to collect external target telemetry[cite: 12] and map active local virtual infrastructure.

---

## Phase 1: Passive Reconnaissance & Target Footprinting
* **Target Domain:** `networkwalks.com`[cite: 6, 7, 8, 9, 10, 11, 12]
* **Platform:** Kali Linux[cite: 6, 7, 8, 9, 10, 11, 12]

### Executed Commands & Discovered Telemetry

* **Domain Registration Analysis (`whois`)**[cite: 10]
  * **Command:** `whois networkwalks.com`[cite: 10]
  * **Registrar:** GoDaddy.com, LLC[cite: 10]
  * **Name Servers:** `NS6135.HOSTGATOR.COM`, `NS6136.HOSTGATOR.COM`[cite: 10]

* **Web Technology Profiling (`whatweb`)**[cite: 11]
  * **Command:** `whatweb networkwalks.com`[cite: 11]
  * **Target IP:** `192.232.216.135`[cite: 11]
  * **Software Stack:** Apache, WordPress 7.1, Bootstrap 7.1, WordPress Download Manager 3.3.58[cite: 11]

* **DNS Resolution (`nslookup`)**[cite: 9]
  * **Command:** `nslookup networkwalks.com`[cite: 9]
  * **Resolver:** `10.36.30.44#53`[cite: 9]
  * **Resolved Address:** `192.232.216.135`[cite: 9]

* **HTTP Header Inspection (`curl`)**[cite: 8]
  * **Command:** `curl -I https://networkwalks.com`[cite: 8]
  * **Headers Captured:** `Server: Apache`, `x-nginx-cache: WordPress`[cite: 8]
  * **Exposed Paths:** `/wp-json/` REST API endpoints[cite: 8]

* **Web Application Firewall Detection (`wafw00f`)**[cite: 7]
  * **Command:** `wafw00f networkwalks.com`[cite: 7]
  * **WAF Identified:** ModSecurity (SpiderLabs) WAF[cite: 7]

* **DNS Enumeration (`dnsrecon`)**[cite: 6]
  * **Command:** `dnsrecon -d networkwalks.com`[cite: 6]
  * **Result:** Executed domain-wide zone/record discovery routines[cite: 6].

---

## Phase 2: Active Network Discovery & Topology Mapping
* **Target Subnet:** `10.0.2.0/24`[cite: 4, 5]
* **Platform:** Zenmap (Nmap 7.99 GUI on Kali Linux)[cite: 3, 4, 5]

### Subnet Scan Findings
* **Scan Type:** Ping Scan (`nmap -sn 10.0.2.0/24`)[cite: 4, 5]
* **Scan Duration:** 256 IP addresses scanned in 3.53 seconds[cite: 5]
* **Live Hosts Discovered:** 2 Hosts Up[cite: 5]

| Target IP | MAC Address | Interface / Hardware Profile | Latency / Status |
| :--- | :--- | :--- | :--- |
| **10.0.2.2** | `08:00:27:E7:BD:68`[cite: 5] | Oracle VirtualBox Virtual NIC[cite: 5] | Host is up (0.0017s latency)[cite: 5] |
| **10.0.2.3** | *Local Host Interface* | Virtual Machine Adapter[cite: 3, 4, 5] | Host is up[cite: 5] |

### Visual Proof & Evidence

#### 1. Passive Reconnaissance Terminal Execution
![Reconnaissance Terminal Commands](Screenshot (423).png)

#### 2. Zenmap Subnet Scan Output
![Zenmap Ping Scan Output](./screenshots/zenmap_scan.jpg)

#### 3. Network Topology Map
![Zenmap Topology Map](./screenshots/zenmap_topology.jpg)

---

## Defensive Recommendations
1. **Suppress HTTP Headers:** Configure Apache/Nginx to hide explicit version numbers to limit automated footprinting[cite: 8, 11].
2. **Restrict Subnet ICMP:** Apply host firewall rules across `10.0.2.0/24` to restrict ping sweeps and unauthorized discovery[cite: 4, 5].
