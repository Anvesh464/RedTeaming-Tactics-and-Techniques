Finding Netblock Addres From Company Name

You can find NetblockTool on Github.

| 1 2 3 4 5 6 7 8 9 10 11  | \#NetblockTool \#Simple run. Get results from Google dorking and ARIN database: python3 NetblockTool.py Company \#Include the verbose flag to print status updates: python3 NetblockTool.py -v Company \#Extract netblocks owned by your target company’s subsidiaries: python3 NetblockTool.py -v Company -s \#Extract point of contact information: python3 NetblockTool.py -v Company -p \#Get as much information as possible, including netblocks found using wildcard queries, points of contact, geolocation data, and physical addresses: python3 NetblockTool.py -wpgav Company -so  |
|--------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|

![NetblockTool.py output](media/3c99ba90fb14f2e317ad85fba6b86535.png)NetblockTool.py output![NetblockTool.py .csv output example](media/699a58b84cca2e4d78a5a84949186e46.png)NetblockTool.py .csv output example

Finding Assets From IP Databases

Finding IP Address From SSL Certificates on Censys.io

You can use [censys.io](https://search.censys.io/) as one of the fast and creative solutions for detecting IP addresses. With this method, by searching the domain name in the SSL certificates in the [Censys.io](http://censys.io/) database, you can obtain all the addresses that the target domain name is passing through.

![Censys.io searching certificates.](media/6c46b5be6bab6bc7ef816d5ee3d2a11b.png)Censys.io searching certificates.

Or you can use this command. But firstly, you have to install python-censys libary. You can install from [here](https://github.com/censys/censys-python).

| 1 2 3  | python3 -m censys search ' services.tls.certificates.leaf_data.subject.common_name: "example.com"' --index-type hosts \| jq -c '.[] \| {ip: .ip}' \> ip.txt \#You can pars output with this command sed -i 's/[\^0-9,.]\*//g' ip.txt  |
|--------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|

![Using censys libary of python.](media/37ea8213f34e0ca597d34b32eeff9789.png)Using censys libary of python.

Finding Organization ASN & Netblock IP Address with BGP

You can find out the Autonomous System Number (ASN) number by searching the keywords of the Organization through the application of BGP [here](https://bgp.he.net/).

![Finding Organization ASN & Netblock IP Address with BGP](media/9d9b70ebab52e5e2f5b3992e5c93bda8.png)Finding Organization ASN & Netblock IP Address with BGP

Finding Netblock IP Address CIDR with nslookup & whois

With the Whois information, a lot of information about the domain name can be accessed. Our goal in this technique is to detect Netblock and CIDR addresses to expand the attack surface. For this, after the address is detected with the help of nslookup, a whois query is sent to this address and the Netblock and CIDR to which this IP address belongs are detected.

In order to expand the attack surface as much as possible in the target organization, we first need the domain and subdomain addresses. Before applying this method, you should collect as many domains and subdomains as possible.

![A screenshot of a computer Description automatically generated](media/c5bf9dbced620c881a2250517c31d8d3.png)Finding Netblock IP Address CIDR with nslookup & whois

![A screenshot of a computer Description automatically generated](media/2125d2669828d98e1c3207c7849aaf1d.png)Finding Netblock IP Address CIDR with nslookup & whois
