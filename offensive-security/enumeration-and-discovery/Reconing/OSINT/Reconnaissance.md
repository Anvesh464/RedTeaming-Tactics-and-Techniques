**Reconnaissance**

Last modified: 2024-09-25

Basic reconnaisance flows.

[**Automation**](https://exploit-notes.hdks.org/exploit/reconnaissance/#automation)

-   [AutoRecon](https://github.com/Tib3rius/AutoRecon)
-   [FinalRecon](https://github.com/thewhiteh4t/FinalRecon)
-   [recon-ng](https://github.com/lanmaster53/recon-ng)
-   [reconftw](https://github.com/six2dez/reconftw)
-   [theHarvester](https://github.com/laramies/theHarvester)

[**Acquisitions**](https://exploit-notes.hdks.org/exploit/reconnaissance/#acquisitions)

We need to find the other companies which are owned by the target company.

-   [CrunchBase](https://www.crunchbase.com/)

[**ASN**](https://exploit-notes.hdks.org/exploit/reconnaissance/#asn)

An autonomous system number (ASN) is a collection of connected IP routing prefixes under the control of network operators. It is assigned to an autonomous system (AS) by the **Internet Assigned Numbers Authority (IANA)**.  
**Border Gateway Protocol (BGP)** is used to notify the routing policy to the other AS or routers.  
We can also find IP ranges belonging to the ASN.

-   [BGP Toolkit](https://bgp.he.net/)
-   [ASN Lookup](https://asnlookup.com/)

[**WHOIS**](https://exploit-notes.hdks.org/exploit/reconnaissance/#whois)

whois is used to find information about the registered users of the domain.

whois example.com

**Copied!**

[**Archived Web Pages**](https://exploit-notes.hdks.org/exploit/reconnaissance/#archived-web-pages)

[Wayback Machine](http://web.archive.org/) is an online tool that archives a lot of websites.

[**Subnet Scan**](https://exploit-notes.hdks.org/exploit/reconnaissance/#subnet-scan)

You need only the **ping scan (skip port scan)** by adding the option **"-sP"**.

*\# /24 - 255.255.255.0*

nmap -sP \<target-ip\>/24 -T2

*\# /16 - 255.255.0.0*

nmap -sP \<target-ip\>/16 -T2

*\# /8 - 255.0.0.0*

nmap -sP \<target-ip\>/8 -T2

**Copied!**

[**Port Scan**](https://exploit-notes.hdks.org/exploit/reconnaissance/#port-scan)

See [Port Scan](https://exploit-notes.hdks.org/exploit/reconnaissance/port-scan/) for details.

[**Subdomains**](https://exploit-notes.hdks.org/exploit/reconnaissance/#subdomains)

See also [Subdomain Discovery](https://exploit-notes.hdks.org/exploit/reconnaissance/subdomain/subdomain-discovery/), [DNS Pentesting](https://exploit-notes.hdks.org/exploit/dns/).

[**Google Search**](https://exploit-notes.hdks.org/exploit/reconnaissance/#google-search)

For example, input site:facebook.com in the search form. We should see a list of subdomains for the facebook.com.

[**VirusTotal**](https://exploit-notes.hdks.org/exploit/reconnaissance/#virustotal)

For example, input "facebook.com" in the search form of the URL section. We shoud see a list of subdomains for the facebook.com in the RELATIONS section.

-   **Subdomain Takeover**

It allows an adversary to claim and take control of the victim's subdomain.

Resource: [OWASP](https://owasp.org/www-project-web-security-testing-guide/latest/4-Web_Application_Security_Testing/02-Configuration_and_Deployment_Management_Testing/10-Test_for_Subdomain_Takeover)

[**Social Accounts**](https://exploit-notes.hdks.org/exploit/reconnaissance/#social-accounts)

We can get more information if the organization uses social platforms as below.

-   Discord
-   Facebook
-   GitHub
-   Mastodon
-   Reddit
-   Twitter

[**Trace Route Packets**](https://exploit-notes.hdks.org/exploit/reconnaissance/#trace-route-packets)

To track the route packets from our IP to target host, run the following command.

traceroute example.com

**Copied!**

[**Find Vulnerabilites**](https://exploit-notes.hdks.org/exploit/reconnaissance/#find-vulnerabilites)

[**Automation**](https://exploit-notes.hdks.org/exploit/reconnaissance/#automation-1)

-   **Nuclei**

[Nuclei](https://github.com/projectdiscovery/nuclei) is a vulnerability scanner based on simple YAML based DSL.

nuclei -h

**Copied!**

[**Exploit DB**](https://exploit-notes.hdks.org/exploit/reconnaissance/#exploit-db)

You can search vulnerabilites written in Exploit-DB by using "searhsploit".

searchsploit \<keyword\>

**Copied!**

If you found vulnerabilities of target, copy them to current directory.  
For example,

searchsploit -m windows/remote/42031.py

*\# or*

searchsploit -m 42031

**Copied!**

[Exploit-DB](https://www.exploit-db.com/) is a database of exploits.  
Find the exploit and download it. For example:

wget https://www.exploit-db.com/raw/42966 -O exploit.py

**Copied!**

Format the exploit code for UNIX.

dos2unix exploit.py

*\# Manual converting*

sed -i 's/\\r//' example.py

**Copied!**

**References**

-   <https://owasp.org/www-project-web-security-testing-guide/latest/4-Web_Application_Security_Testing/02-Configuration_and_Deployment_Management_Testing/10-Test_for_Subdomain_Takeover>
