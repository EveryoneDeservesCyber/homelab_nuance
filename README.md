# homelab_nuance
My homelab journey with enterprise-level capabilities (mistakes will be made)

## Executive Summary
**Objective:** Start with learning and discovery before taking action. Focus on reading documentation, using videos, and getting to the "why" when needed. 

**End state:** A fully functioning server, built in isolation, that acts as my homelab. Appropriately titled "Rome".

## Research
* Learning the ins and outs of my server. Two great picks: how RAM is loaded properly in a server and why. *White is the start of the memory channel...
* Understanding the importance of iDRAC and setting that up first
* Proxmox VE vs VMware ESXi
* Options for my Raspberry Pi; settling on making them vulnerable endpoints
* Researching SIEM
* Researching IPS/IDP

## Tech Stack & Topology
### Infrastructure & Tools
*   **Hypervisor:** PROXMOX VE with VMware ESXi running in a dedicated VM
*   **SIEM / Logging:** TBD.
*   **Firewall / Routing:** TBD
*   **Endpoints:** TBD
*   **Threat Intel / Frameworks:** [e.g., OpenCTI, MITRE ATT&CK]


## DRAFT Network Diagram

<img width="559" height="533" alt="image" src="https://github.com/user-attachments/assets/848897df-8c03-4fc7-9fa4-91fe9c43608a" />

## First Steps
* Researching and understanding a physical server requires some patience and understanding. I spent about a week mapping my homelab architecture, identifying how I was going to establish networks, and learning about my Dell R640. Small details matter, like knowing how to install RAM, an SSD, etc.
* Using the Dell website, YouTube, and LLMs, I learned about the power of iDRAC and setting up the Lifecycle Controller. Great video here: https://www.youtube.com/watch?v=-adahtszQXA
* Once I learned the basics about my server, I understood how I wanted to set it up in my open rack and properly applied the general network information through the iDRAC9 Dashboard.
* From there, I used iDRAC9 to update my server. The process was fairly simple with iDRAC9, but I learned that I needed a DNS address like 1.1.1.1 or 8.8.8.8 to access Dell downloads through iDRAC's remote capability. The process was fairly straightforward and allowed me to learn how loud my single server can get. _Note:_ The iDRAC firmware took the longest to update and reboot.
* _Note_: Restarting your server too many times, as I did with all of my updates, can throw your iDRAC into Recovery Mode. Here is the fix: https://www.dell.com/support/kbdoc/en-us/000136186/lifecycle-controller-update-required-lc-is-in-recovery-mode
* 
