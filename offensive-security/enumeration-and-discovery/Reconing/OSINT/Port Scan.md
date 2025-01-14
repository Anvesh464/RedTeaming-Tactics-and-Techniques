Port Scanning is a port mapping on the network. It is often executing when reconnaissance.

[**Nmap**](https://exploit-notes.hdks.org/exploit/reconnaissance/network/port-scan/#nmap)

Nmap is still the most commonly used tool when scanning ports of the target system.  
But in recent years, some other tools, such as masscan or rustscan, are also becoming popular because the tools scan faster than nmap.

It's recommened to do as stealth scan (SYN scan) by adding the option -sS.  
Also it's prefered to add -T2 flag for being polite.

*\# -sS: SYN Scan*

*\# -sV: Service/Version detection*

*\# -sC: Default NSE (script)*

*\# -T2: Timing template.*

*\# -p-: Scan all ports*

sudo nmap -sSVC -p- \<target-ip\> -T2

sudo nmap -sSVC -p 1-65535 \<target-ip\>

*\# -p 1000-1500: Scan ports from 1000 to 1500*

sudo nmap -sSVC -p 1000-1500 \<target-ip\>

*\# If port scanning on CTF not real organization, use \`--min-rate\` for increase scan speed.*

*\# --min-rate: Send packets no slower than \<number\> per second*

sudo nmap -sSVC -p- \<target-ip\> --min-rate 1000

*\# -A: All detection*

sudo nmap -sS -A \<target-ip\>

**Copied!**

[**UDP Scan**](https://exploit-notes.hdks.org/exploit/reconnaissance/network/port-scan/#udp-scan)

Sometimes you need the UDP scan.

nmap -sU --top-ports 25 \<target-ip\>

nmap -sU --top-ports 50 --open \<target-ip\>

**Copied!**

[**Skip Host Discovery**](https://exploit-notes.hdks.org/exploit/reconnaissance/network/port-scan/#skip-host-discovery)

sudo nmap -sS -Pn \<target-ip\>

**Copied!**

[**Specified Ports**](https://exploit-notes.hdks.org/exploit/reconnaissance/network/port-scan/#specified-ports)

*\# -p 22,80,88: Scan only 22, 80, 88 ports*

sudo nmap -sSVC -p 22,80,88

*\# --top-ports: Scan top 100 ports*

sudo nmap -sS --top-ports 100 \<target-ip\>

*\# -p-1000: Scan first 1000 ports*

sudo nmap -sS -p-1000 \<target-ip\>

**Copied!**

[**Network Ranges**](https://exploit-notes.hdks.org/exploit/reconnaissance/network/port-scan/#network-ranges)

*\# Wildcard*

nmap 10.0.0.\*

*\# CIDR (Classless Inter-Domain Routing)*

nmap 10.0.0.1/24

**Copied!**

[**Scan Techniques**](https://exploit-notes.hdks.org/exploit/reconnaissance/network/port-scan/#scan-techniques)

*\# FIN scan*

nmap -sF \<target-ip\>

*\# Xmas scan*

nmap -sX \<target-ip\>

**Copied!**

[**Firewall Bypass**](https://exploit-notes.hdks.org/exploit/reconnaissance/network/port-scan/#firewall-bypass)

*\# Fragmented packets*

nmap -f \<target-ip\>

*\# Specify MTU (Maximum Transmission Unit)*

nmap --mtu 16 \<target-ip\>

nmap --mtu 24 \<target-ip\>

*\# Decoy*

nmap -D RND:3 \<target-ip\>

**Copied!**

[**Nmap Scripting Engine (NSE)**](https://exploit-notes.hdks.org/exploit/reconnaissance/network/port-scan/#nmap-scripting-engine-(nse))

nmap -sC \<target-ip\>

nmap --script vuln \<target-ip\>

**Copied!**

[**Using Proxychains**](https://exploit-notes.hdks.org/exploit/reconnaissance/network/port-scan/#using-proxychains)

First start Tor service.

sudo service tor start

sudo service tor status

**Copied!**

To execute the nmap with proxychains, add the proxychains command before the nmap command.

sudo proxychains nmap -sS \<target-ip\>

**Copied!**

[**Port Knocking**](https://exploit-notes.hdks.org/exploit/reconnaissance/network/port-scan/#port-knocking)

Port knocking is a method of establishing a connection to a networked computer that has no open ports.

**for** i **in** \<port_1\> \<port_2\> \<port_3\>;**do** nmap -Pn -p \$i --host-timeout 201 --max-retries 0 \<target-ip\>;**done**

*\# or we can use \`curl\` command for knocking ports.*

*\# -m: max time in seconds*

curl \<ip\>:\<port1\> -m 1

curl \<ip\>:\<port2\> -m 1

curl \<ip\>:\<port3\> -m 1

**Copied!**

After that, check if ports opened.

nmap \<target-ip\>

**Copied!**

[**Massscan**](https://exploit-notes.hdks.org/exploit/reconnaissance/network/port-scan/#massscan)

[**Masscan**](https://github.com/robertdavidgraham/masscan) is a TCP port scanner. It is faster than nmap.

masscan \<target-ip\>/16

masscan \<target-ip\>/24

*\# -p: Ports*

masscan \<target-ip\>/16 -p 80,443

masscan \<target-ip\>/16 -p 22-80

masscan \<target-ip\>/16 -p 0-65535

*\# --top-ports*

masscan \<target-ip\>/16 --top-ports 100

**Copied!**

[**RustScan**](https://exploit-notes.hdks.org/exploit/reconnaissance/network/port-scan/#rustscan)

[**RustScan**](https://github.com/RustScan/RustScan) is the modern port scanner. It is faster than nmap.

*\# -a: Addresses*

*\# --ulimit: Limit system resource amounts*

rustscan -a \<target-ip-1\>,\<target-ip-2\> --ulimit 5000

rustscan -a 'hosts.txt' --ulimit 5000

*\# CIDR*

rustscan -a 192.168.0.0/30

*\# -p: Ports*

rustscan -a \<target-ip\> -p 22,80

*\# Using Docker image (recommended way by the RustScan official)*

*\# -u 0: Run as root*

*\# -it: Interactive mode*

*\# --rm: Remove the container after finishing to execute*

docker run -u 0 -it --rm --name rustscan rustscan/rustscan:2.1.1 -a \<target-ip\> -- -sSVC

**Copied!**

We can also use the Nmap arguments as below.

rustscan -a \<target-ip\> -- -sSVC

rustscan -a \<target-ip\> -- -sS -A

**Copied!**

[**Naabu**](https://exploit-notes.hdks.org/exploit/reconnaissance/network/port-scan/#naabu)

*\# -p -: Scan all ports*

naabu -p - -host \<target-ip\>

*\# -sD: Service discovery \*under development [2024-02-11]*

*\# -sV: Service version \*under development [2024-02-11]*

naabu -sD -s -p 22,80,443 -host \<target-ip\>

**Copied!**

**References**

-   <https://nmap.org/book/nmap-defenses-trickery.html>
-   <https://refabr1k.gitbook.io/oscp/info-gathering/port-knocking>
