# Findings - Cyber Task 1

*Scanned network:* xxx.xxx.xxx.xxx/24  
*Date:* 22 Sept 2025  

---

## Host: 10.60.108.70
- *MAC Address:* MAC_REDACTED (Unknown vendor)
- *Open ports:*
  - 53/tcp → DNS (SOFTWARE_REDACTED)
- *Observations:*
  - The host is running a DNS service.
  - SOFTWARE_REDACTED is outdated (current versions are significantly newer).
- *Risks:*
  - Outdated dnsmasq versions have known vulnerabilities (e.g., DNS cache poisoning, DoS).
  - An open DNS service could be abused for DNS amplification attacks if exposed beyond LAN.
- *Remediation:*
  - Update dnsmasq to the latest stable version.
  - Restrict DNS queries to trusted devices only.
  - Use firewall rules to block external access.

---

## Host: 10.60.108.117
- *MAC Address:* MAC_REDACTED (Unknown vendor)
- *Open ports:* None detected (all scanned ports closed).
- *Observations:*
  - Device is reachable but no open TCP ports were found.
- *Risks:*
  - Minimal exposure; still could be vulnerable on UDP ports or if firewall is misconfigured.
- *Remediation:*
  - Keep device patched and updated.
  - Ensure unused services remain disabled.
  - Periodically rescan to detect future changes.

---

## Host: 10.60.108.250
- *MAC Address:* Not shown (likely your scanning Windows machine).
- *Open ports:*
  - 135/tcp → Microsoft RPC (MSRPC)
  - 139/tcp → NetBIOS Session Service
  - 445/tcp → Microsoft-DS / SMB
  - 3306/tcp → MySQL (unauthorized)
  - 9999/tcp → Abyss? (identified as Tally License Server, Gateway v11.0 / Release 5.1.0)
- *Observations:*
  - Windows host with SMB and RPC services enabled.
  - MySQL service accessible but requires authentication.
  - Port 9999 runs a TallyPrime-related license server, exposing detailed version and product information.
- *Risks:*
  - SMB (ports 139/445) has a long history of critical vulnerabilities (e.g., EternalBlue).
  - RPC services (port 135) may expose the system to privilege escalation exploits.
  - MySQL (3306) exposure may lead to brute-force attempts or data leaks if misconfigured.
  - Tally license server banner leaks internal product/version details (information disclosure).
- *Remediation:*
  - Restrict SMB and RPC access to trusted subnets only.
  - Apply latest Windows updates and SMB hardening (require SMB signing, disable SMBv1).
  - Restrict MySQL access to localhost or trusted hosts; enforce strong authentication.
  - If the Tally license service is not required externally, bind it to localhost or firewall it.
  - Regularly review firewall rules and close unnecessary ports.

---

## Summary
- *3 hosts detected* in the subnet:  
  - 1 DNS server (10.60.108.70) with outdated software.  
  - 1 host with no open ports (10.60.108.117).  
  - 1 Windows host (10.60.108.250) with multiple critical services exposed (SMB, MySQL, Tally license server).  

*Overall Risk:* Medium to High.  
- Exposure of SMB and MySQL increases attack surface.  
- Outdated dnsmasq DNS server may be vulnerable.  

*Recommendations:*  
- Patch and update all services.  
- Limit exposure with host-based firewall rules.  
- Disable or restrict unnecessary services (especially SMB and MySQL).  
- Monitor with periodic re-scanning.