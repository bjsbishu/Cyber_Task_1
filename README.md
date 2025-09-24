# Cyber_Task_1
Cyber Task 1 - Port scanning
Summary

Performed port scanning on my home network (xxx.xxx.xxx.xxx/24) using Nmap to discover live host, open ports, and services. All scanning was performed only on devices I own.

Command used

discovery (live host)

nmap -sn xxx.xxx.xxx.xxx/24 -oN discovery.txt

Full TCP SYN scan with service detection and default scripts


nmap -sS -sV -sC xxx.xxx.xxx.xxx/24 -oN scan_results.txt -oX scan_results.xml -oG scan_result.gnmap

files included


discovery.txt
scan_result.txt
scan_result.gnmap
scan_result.xml
capture.pcapng
findings.md

Notes


Scanned only my home network and my own devices.
Follow-up remediation recommendations include in findings.md
