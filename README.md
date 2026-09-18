# Network Reconnaissance & Subnet Discovery Operations

## Project Overview
This repository details the execution of two foundational cybersecurity operational phases: **Passive Footprinting & Reconnaissance** using Kali Linux CLI utilities and **Active Subnet Discovery** using Zenmap. The objective was to collect external target telemetry and map active local virtual infrastructure.

---

## Phase 1: Passive Reconnaissance & Target Footprinting
* **Target Domain:** `networkwalks.com`
* **Platform:** Kali Linux

### Executed Commands & Discovered Telemetry

* **Domain Registration Analysis (`whois`)**
  * **Command:** `whois networkwalks.com`
  * **Registrar:** GoDaddy.com, LLC
  * **Name Servers:** `NS6135.HOSTGATOR.COM`, `NS6136.HOSTGATOR.COM`

* **Web Technology Profiling (`whatweb`)**
  * **Command:** `whatweb networkwalks.com`
  * **Target IP:** `192.232.216.135`
  * **Software Stack:** Apache, WordPress 7.1, Bootstrap 7.1, WordPress Download Manager 3.3.58

* **DNS Resolution (`nslookup`)**
  * **Command:** `nslookup networkwalks.com`
  * **Resolver:** `10.36.30.44#53`
  * **Resolved Address:** `192.232.216.135`

* **HTTP Header Inspection (`curl`)**
  * **Command:** `curl -I https://networkwalks.com`
  * **Headers Captured:** `Server: Apache`, `x-nginx-cache: WordPress`
  * **Exposed Paths:** `/wp-json/` REST API endpoints

* **Web Application Firewall Detection (`wafw00f`)**
  * **Command:** `wafw00f networkwalks.com`
  * **WAF Identified:** ModSecurity (SpiderLabs) WAF

* **DNS Enumeration (`dnsrecon`)**
  * **Command:** `dnsrecon -d networkwalks.com`
  * **Result:** Executed domain-wide zone/record discovery routines

### Reconnaissance Evidence
<!-- Drag and drop your terminal screenshot here in GitHub editor -->

---

## Phase 2: Active Network Discovery & Topology Mapping
* **Target Subnet:** `10.0.2.0/24`
* **Platform:** Zenmap (Nmap 7.99 GUI on Kali Linux)

### Subnet Scan Findings
* **Scan Type:** Ping Scan (`nmap -sn 10.0.2.0/24`)
* **Scan Duration:** 256 IP addresses scanned in 3.53 seconds
* **Live Hosts Discovered:** 2 Hosts Up

| Target IP | MAC Address | Interface / Hardware Profile | Latency / Status |
| :--- | :--- | :--- | :--- |
| **10.0.2.2** | `08:00:27:E7:BD:68` | Oracle VirtualBox Virtual NIC | Host is up (0.0017s latency) |
| **10.0.2.3** | *Local Host Interface* | Virtual Machine Adapter | Host is up |

### Scan & Topology Evidence
<https://github.com/advocals/Cybersecurity-Reconnaissance-Network-Discovery-Lab/blob/main/Screenshot%20(424).png>

---

## Defensive Recommendations
1. **Suppress HTTP Headers:** Configure Apache/Nginx to hide explicit version numbers to limit automated footprinting.
2. **Restrict Subnet ICMP:** Apply host firewall rules across `10.0.2.0/24` to restrict ping sweeps and unauthorized discovery.
