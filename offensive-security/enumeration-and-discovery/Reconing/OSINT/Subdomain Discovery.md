Finding subdomains is a method of reconnaissance.

[**Online Tools**](https://exploit-notes.hdks.org/exploit/reconnaissance/subdomain/subdomain-discovery/#online-tools)

-   [Subdomain Finder](https://subdomainfinder.c99.nl/)
-   [nmmapper](https://www.nmmapper.com/)

[**Automation**](https://exploit-notes.hdks.org/exploit/reconnaissance/subdomain/subdomain-discovery/#automation)

Reference: [How to find subdomain takeover using httpx + dig](https://medium.com/@DrakenKun/how-to-find-subdomain-takeover-using-httpx-dig-5c2351d380b4)

[**Subfinder**](https://exploit-notes.hdks.org/exploit/reconnaissance/subdomain/subdomain-discovery/#subfinder)

To set API keys, add them to \$HOME/.config/subfinder/provider-config.yaml. See [the ProjectDiscovery's Documentation](https://docs.projectdiscovery.io/tools/subfinder/install#post-install-configuration) for details.

*\# -all: Use all sources for enumeration*

*\# -cs: Include all sources in the output*

subfinder -d example.com -all -cs \> tmp.txt ; cat tmp.txt \| cut -d "," -f 1 \> domains.txt ; rm tmp.txt

**Copied!**

[**BBOT**](https://exploit-notes.hdks.org/exploit/reconnaissance/subdomain/subdomain-discovery/#bbot)

bbot -t example.com -f subdomain-enum

*\# After enumerating, see the result file at \~/.bbot/scans/xxxx_xxxx/subdomains.txt*

**Copied!**

[**Google Dorks**](https://exploit-notes.hdks.org/exploit/reconnaissance/subdomain/subdomain-discovery/#google-dorks)

Use site: parameter on Google search.

site:example.com

site:\*.example.com

site:\*.\*.example.com

*\# Subdomains including hyphen ('-') e.g. api-dev.example.com*

site:\*-\*.example.com

*\# Exclude 'www' domain*

site:\*.example.com -site:www.example.com

**Copied!**

[**Subdomain Takeover**](https://exploit-notes.hdks.org/exploit/reconnaissance/subdomain/subdomain-discovery/#subdomain-takeover)

After enumerating, it’s worth to check the [Subdomain Takever](https://exploit-notes.hdks.org/exploit/reconnaissance/subdomain/subdomain-takeover/).
