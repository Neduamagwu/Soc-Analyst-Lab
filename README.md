# SOC Analyst Lab

My hands-on SOC analyst home lab and investigation notes.

## About This Lab

This repository documents my practical learning journey toward becoming a SOC analyst.

The lab includes:

- Windows 11
- Kali Linux
- Metasploitable 2
- pfSense
- VMware Workstation
- Wireshark
- Splunk
- Wazuh (planned)

## Network Lab

The isolated SOC lab uses a VMware Host-only network:

- Network: `192.168.8.0/24`
- pfSense LAN: `192.168.8.1`
- Kali Linux: `192.168.8.100`
- Metasploitable 2: `192.168.8.101`
- Windows Host Adapter: `192.168.8.2`

## Investigations Completed

### Wireshark

- ARP analysis
- ICMP analysis
- DNS analysis
- TCP three-way handshake
- HTTP GET and HEAD requests
- HTTP status codes
- Nmap SYN scan traffic
- DVWA login traffic
- HTTP POST request analysis
- PHP session cookie analysis

## SOC Investigation Method

I am practicing the following investigation approach:

1. Observation
2. Context
3. Evidence
4. Assessment

An alert or unusual event is treated as a clue rather than an immediate conclusion.

## Current Progress

- [x] Build isolated VMware network
- [x] Configure pfSense
- [x] Configure Kali Linux
- [x] Configure Metasploitable 2
- [x] Learn basic networking concepts
- [x] Perform Wireshark investigations
- [x] Analyze HTTP traffic
- [x] Analyze DVWA login traffic
- [ ] Deploy Wazuh
- [ ] Configure Windows endpoint monitoring
- [ ] Build detection rules
- [ ] Practice SOC investigations
- [ ] Document incident-response exercises
