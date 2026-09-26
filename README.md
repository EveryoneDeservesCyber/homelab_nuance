# homelab_nuance
My homelab journey with enterprise-level capabilities (mistakes will be made)

## Executive Summary
**Objective:** Start with learning and discovery before taking action. Focus on reading documentation, using videos, and getting to the "why" when needed. This will be a deliberate process, as it is a personal project to build an environment where I can learn, test, and experiment in an enterprise-like setting on a personally owned server. I have experience with VMware ESXi, but I'm new to Proxmox VE...so I want to enjoy the learning journey with no real timeline.

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


## DRAFT Network Diagram (will clean up once i finalize)

<img width="559" height="533" alt="image" src="https://github.com/user-attachments/assets/848897df-8c03-4fc7-9fa4-91fe9c43608a" />

## First Steps
* Researching and understanding a physical server requires some patience and understanding. I spent about a week mapping my homelab architecture, figuring out how I would establish networks, and learning about my Dell R640. Small details matter, like knowing how to install RAM, an SSD, etc.
* Using the Dell website, YouTube, and LLMs, I learned about the power of iDRAC and setting up the Lifecycle Controller. Great video here: https://www.youtube.com/watch?v=-adahtszQXA
* Once I learned the basics about my server, I understood how I wanted to set it up in my open rack and properly applied the general network information through the iDRAC9 Dashboard.
* From there, I used iDRAC9 to update my server. The process was fairly simple with iDRAC9, but I learned that I needed a DNS address like 1.1.1.1 or 8.8.8.8 to access Dell downloads through iDRAC's remote capability. The process was fairly straightforward and let me see how loud my single server can get. _Note:_ The iDRAC firmware took the longest to update and reboot.
* _Note_: Restarting your server too many times, as I did with all of my updates, can throw your iDRAC into Recovery Mode. Here is the fix: https://www.dell.com/support/kbdoc/en-us/000136186/lifecycle-controller-update-required-lc-is-in-recovery-mode

  ##Second Steps - Loading Proxmox VE
  * I intended to use a bootable USB for loading Proxmox VE, but I learned about the ability to do it through IDRAC and the Virtual Media. I had to troubleshoot the mapping because my Lifecycle Controller booted into Recovery mode, but after I cleared that, it was a simple, easy process; I highly recommend it over going to the server and inserting a USB.
  * Once I completed the Proxmox VE install, I hit another wall. My target disk wouldn't let me install Proxmox...turns out, a refurbished server can carry data or info from the previous owner. I had to research how to check my virtual and physical disks, then create a new VD. Google, Claude, and Dell helped me learn all these interesting concepts.
  * I ran into another issue; my Micron MTFDDAV drives are not compatible with kernel 6.17+ for Proxmox VE 9.2. It looks like I am going to an older version, 8.4, until there is a fix/patch. This forum and Google were my friends: https://forum.proxmox.com/threads/pve-9-1-running-on-a-boss-s1-causing-i-o-errors-and-filesystem-remounts-as-r-o.181296/
  * Currently installing Proxmox VE 8.4...
  
* Third Steps - Updating Proxmox
* Since I do not have the enterprise version of Proxmox VE, I needed to ensure I changed repositories so I could actually pull information.
* Using the documentation pages, I learned about switching the package repository it pulls from for non-subscription members. https://pve.proxmox.com/wiki/Package_Repositories
* After updating and upgrading, I created a non-admin account to work out of and then confirmed/disabled direct root SSH capability to harden.
*   nano /etc/ssh/sshd_config...change PermitRootLogin no
*   _Note:_ I read something about confirming my made user account could SSH in before turning this out so I don't lock myself out. Good point to always remember. Test made accounts before turning something off for other accounts. I also learned about a PermitRootLogin prohibit-password option. In my smaller VM homelabs, I never worried about such things because I would fire and forget for single-purpose use.
* I've spent the last week or two assessing my cable management and setting up my UPS. While I am OCD about cables, I'm not worried about "pretty" as much as I am worried about organization.
* Did some remote SSH'ing in via a MacBook Pro 13 that I repurposed with Ubuntu LTS...running like a dream...the MAC, that is. I will probably update the Network Architecture next month after I figure out any additional systems I want to add. I am experimenting with PoE with my Raspberry Pis and building a Raspberry Pi out for Wardriving...so I need to finish up the side quest and get back to it.
* Reading and comparing my Firewall options now. Determining if I still want to use OPNsense
