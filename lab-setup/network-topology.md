# SOC Lab Network Topology

## Overview

The SOC lab is built using VMware Workstation and uses an isolated Host-only network for communication between the lab systems.

## Network

- Network: `192.168.8.0/24`
- pfSense LAN: `192.168.8.1`
- Kali Linux: `192.168.8.100`
- Metasploitable 2: `192.168.8.101`
- Windows Host Adapter: `192.168.8.2`

## Lab Systems

### pfSense

pfSense acts as the firewall and router for the isolated SOC lab.

- LAN: `192.168.8.1`
- Provides DHCP to the lab network
- Provides routing between the lab network and WAN
- WAN uses VMware NAT

### Kali Linux

Kali Linux is used as the analyst/attacker workstation for controlled lab exercises.

- IP: `192.168.8.100`
- Network interface: `eth0`
- Tools used include Wireshark and Nmap

### Metasploitable 2

Metasploitable 2 is an intentionally vulnerable machine used as the target for security testing and traffic analysis.

- IP: `192.168.8.101`
- Connected only to the isolated Host-only network

### Windows

The Windows host participates in the lab through the VMware Host-only adapter.

- VMnet1 adapter: `192.168.8.2`

## Topology

                    Internet
                       |
                 Home Router
                       |
                Windows Host
                       |
                  VMware NAT
                       |
                pfSense WAN
                       |
              pfSense LAN
               192.168.8.1
                       |
                 VMnet1
              192.168.8.0/24
                 /     |     \
                /      |      \
       Kali .100   Meta .101   Windows .2

Purpose

The isolated network allows security monitoring, scanning, packet capture, and investigation exercises to be 
performed without exposing the intentionally vulnerable Metasploitable system to the physical home network.
