# 🔧 Windows 11 Ethernet Failure Troubleshooting & Diagnostic Walkthrough

## 📘 Summary
In this lab, I performed a structured troubleshooting workflow to diagnose and resolve an Ethernet connectivity issue on a Windows 11 system. I began by validating the physical connection and link activity, then confirmed the adapter status inside Windows. I proceeded with a full IP stack and Winsock reset, inspected DHCP and DNS configuration, and finally tested manual DNS assignment to isolate name-resolution failures.  

---

# 🚀 Troubleshooting Steps

## 🔍 Step 1 — Physical Cable & Link Verification
I started by inspecting the Ethernet cable and ensuring both ends were fully inserted. I checked the NIC link lights, tested a different LAN port on the router, and swapped in a known-good cable to rule out physical failures.

>**📝Notes**
>- Link lights confirm Layer 1 and Layer 2 activity.  
>- No link light typically means a bad cable, failing NIC, or faulty router port.  
>- Physical inspection should always be the first step before software troubleshooting.

---

## 🔄 Step 2 — Reseating the Cable & Testing Alternate Ports
I reseated the Ethernet cable on both the PC and router to eliminate loose connection issues. I then connected the cable to a different LAN port to determine whether a specific port was causing the problem.

>**📝Notes**
>- Reseating helps remove intermittent contact faults.  
>- Switching ports isolates potential router hardware failures.  
>- This ensures the issue is not caused by a simple physical layer fault.

---

## 🖥️ Step 3 — Validating the Ethernet Adapter in Windows
I opened Network Connections using `ncpa.cpl` and disabled then re-enabled the Ethernet adapter to force it to reinitialize and restart DHCP negotiation. I observed status messages such as "Identifying..." or "Unidentified network."

<img width="400" height="199" alt="GNUOrz2" src="https://github.com/user-attachments/assets/2c5b2d99-d883-4c53-bb8a-de6c85a31db6" />

---

<img width="361" height="452" alt="H0lJ5um" src="https://github.com/user-attachments/assets/6cc860dd-722d-4ab3-a70f-e11a6d5207a3" />

>**📝Notes**
>- “Identifying…” indicates Windows is performing DHCP negotiation.  
>- “Unidentified network” usually means missing or invalid IP or DNS.  
>- Reinitializing the adapter clears temporary driver or OS-level network issues.

---

## 🧹 Step 4 — Resetting IP Stack, Winsock, and DNS Cache
The troubleshooting steps follow a methodical approach to fix Ethernet issues in Windows 11. They cover checking physical connections, verifying the adapter, resetting the network stack, and testing IP and DNS settings to systematically identify and resolve both hardware and software problems.

<img width="509" height="721" alt="DUCkPMy" src="https://github.com/user-attachments/assets/72a580b7-e3c0-4eaf-a2ee-345e0ae7525a" />

---

<img width="505" height="98" alt="9oLG66f" src="https://github.com/user-attachments/assets/7d2d13a6-fef3-4d5c-bc76-58cbd8b4f946" />

---

<img width="736" height="810" alt="WsnlF5e" src="https://github.com/user-attachments/assets/86e87cd3-a596-49db-b9c0-d80f4cbb5673" />

---

<img width="718" height="132" alt="sG2uIxp" src="https://github.com/user-attachments/assets/41b2fb6d-460e-405c-b66b-d2e449c5de4f" />

>**📝Notes**
>- `netsh winsock reset` repairs corrupted Windows networking APIs.  
>- `netsh int ip reset` rebuilds the TCP/IP configuration.  
>- `ipconfig /flushdns` removes cached DNS entries.  
>- `ipconfig /release` releases the current DHCP-assigned IP.  
>- `ipconfig /renew` requests a new DHCP IP from the server.

---

## 📡 Step 5 — Inspecting IP Address, Gateway, and DNS
I ran `ipconfig` to view the system’s IPv4 address, subnet mask, default gateway, and DNS configuration to check for DHCP assignment or APIPA fallback.

<img width="661" height="494" alt="FTY9wCA" src="https://github.com/user-attachments/assets/53578971-ad30-4789-91c6-a1b60aeb3452" />

>**📝Notes**
>- Valid private DHCP ranges: `192.168.x.x`, `10.x.x.x`, `172.16–31.x.x`.  
>- `169.254.x.x` indicates APIPA and DHCP failure.  
>- Missing DNS entries prevent domain name resolution even if IP connectivity exists.

---

## 🌐 Step 6 — Manually Assigning DNS for Diagnostic Testing
I manually configured the DNS servers for the Ethernet adapter:  
Preferred: 8.8.8.8  
Alternate: 8.8.4.4

<img width="747" height="460" alt="C1du5O5" src="https://github.com/user-attachments/assets/b95c0151-9c2a-4abb-b3ef-0879d278cb94" />

---

<img width="557" height="249" alt="4USpYlc" src="https://github.com/user-attachments/assets/c87d8687-fe24-434d-a685-66e2da5ea9b3" />

>**📝Notes**
>- Manual DNS helps identify failures in DHCP-provided DNS.  
>- Google DNS servers provide reliable external resolution.  
>- Successful connectivity with manual DNS indicates a gateway DHCP/DNS misconfiguration.

---

## ✅ Conclusion
I followed a structured troubleshooting workflow starting at the physical layer, then progressing through OS-level resets, IP/DNS inspection, and manual DNS testing. This process provided a repeatable method for diagnosing Ethernet failures in Windows 11 across physical, data link, network, and name-resolution layers.
