# DNS NXDOMAIN Investigation

## Objective

Investigate DNS traffic and identify NXDOMAIN responses using Wireshark.

## Lab Environment

- Source: Kali Linux
- Source IP: 192.168.8.100
- DNS resolver: pfSense
- DNS resolver IP: 192.168.8.1
- Interface: eth0
- Tool: Wireshark

## Investigation

A DNS query was generated from Kali for a deliberately nonexistent domain:

`test-1.invalid`

Wireshark showed a DNS response from pfSense with:

- Reply code: No such name (3)
- Answer RRs: 0
- Protocol: DNS

The Wireshark display filter used was:

`dns.flags.rcode == 3`

This filter displayed five NXDOMAIN responses for:

- test-1.invalid
- test-2.invalid
- test-3.invalid
- test-4.invalid
- test-5.invalid

## Observation

Multiple NXDOMAIN responses were generated from the Kali system within a short period.

The traffic was:

`192.168.8.100 → 192.168.8.1`

The responses were:

`192.168.8.1 → 192.168.8.100`

## Assessment

The activity was expected and benign because the DNS queries were intentionally generated as part of the lab exercise.

NXDOMAIN means that the requested domain name does not exist.

A high volume of unusual or random-looking NXDOMAIN requests from an endpoint in a real environment could warrant further investigation for possible malware activity, including possible Domain Generation Algorithm (DGA) behavior.

NXDOMAIN traffic alone is not sufficient to conclude that malware is present.

## Key Learning

DNS reply code 3 represents NXDOMAIN ("No such name").

SOC analysts should investigate the pattern and context of DNS activity rather than treating a single NXDOMAIN response as malicious.
