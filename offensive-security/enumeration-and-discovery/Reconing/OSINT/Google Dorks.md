**Google Dorks**

Last modified: 2023-10-30

Google Dorks are Google searching techniques.

[**Cache/Archive**](https://exploit-notes.hdks.org/exploit/reconnaissance/search-technique/google-dorks/#cache%2Farchive)

Search the latest cached results.

cache:examle.com

**Copied!**

[**Country & Language**](https://exploit-notes.hdks.org/exploit/reconnaissance/search-technique/google-dorks/#country-%26-language)

If we want to get search results with specific country and language, set parameters gl and hl.

*\# gl=us: United States*

*\# hl=en: English*

https://www.google.com/search?q=apple&gl=us&hl=en

**Copied!**

[**Directory Listing**](https://exploit-notes.hdks.org/exploit/reconnaissance/search-technique/google-dorks/#directory-listing)

Search websites which allow directory listings. We can retrieve all files if it's enabled in websites.

intext: "Index of /admin"

intext: "Index of /wp-admin"

site:example.com intext: "Index of /admin"

**Copied!**

[**File Types**](https://exploit-notes.hdks.org/exploit/reconnaissance/search-technique/google-dorks/#file-types)

Specify the filetype e.g. pdf\`.

filetype:pdf

filetype:pdf "email address"

**Copied!**

[**Sensitive Information**](https://exploit-notes.hdks.org/exploit/reconnaissance/search-technique/google-dorks/#sensitive-information)

site:github.com "DB_USER"

site:github.com "DB_PASSWORD"

*\# Filter by datetime*

"DB_USER" after:2022-01-01 before:2023-01-01

**Copied!**

[**Subdomains**](https://exploit-notes.hdks.org/exploit/reconnaissance/search-technique/google-dorks/#subdomains)

site:\*.google.com

*\# -site: Exclude specific domain*

site:\*.example.com -site:www.example.com

*\# Specify file extension*

site:\*.google.com ext:php

**Copied!**

[**Title**](https://exploit-notes.hdks.org/exploit/reconnaissance/search-technique/google-dorks/#title)

Searche keywords contained in page title.

intitle:pentesting

**Copied!**

[**URL**](https://exploit-notes.hdks.org/exploit/reconnaissance/search-technique/google-dorks/#url)

Search all URLs containing specific keyword e.g. TLD (com, eu, io, etc.).

inurl:edu

inurl:edu "login"

**Copied!**

**References**

-   <https://www.exploit-db.com/google-hacking-database>
