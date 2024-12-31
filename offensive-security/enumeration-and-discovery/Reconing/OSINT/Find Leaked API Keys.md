**Find Leaked API Keys**

Last modified: 2023-08-24

Finding API keys which are leaked is crucial work for penetration testing or bug bounty. If we found the API keys leaked, sensitive information is at risk of being stolen. So immediate actions must be taken.

[**Awesome Resources**](https://exploit-notes.hdks.org/exploit/reconnaissance/find-leaked-api-keys/#awesome-resources)

-   [Keyhacks](https://github.com/streaak/keyhacks)

This repository lists quick ways to find API keys of various providers.

[**Google Dorks**](https://exploit-notes.hdks.org/exploit/reconnaissance/find-leaked-api-keys/#google-dorks)

Google Dorks is useful to search leaked API keys/tokens.  
\*Here is the simple example so might be unuseful. Please see Awesome Resources section if you are seriously looking for that.

[**Common APIs**](https://exploit-notes.hdks.org/exploit/reconnaissance/find-leaked-api-keys/#common-apis)

Try changing the site domain and the extensions e.g. js**,** py**,** go.

*\# GitHub repositories*

site:github.com ext:php "api-key"

site:github.com ext:php "api_key"

site:github.com ext:php "api-token"

site:github.com ext:php "api_token"

site:github.com ext:php "access-token"

site:github.com ext:php "access_token"

site:github.com ext:php "x-api-key"

site:github.com ext:php "x_api_key"

site:github.com ext:php "x-api-token"

site:github.com ext:php "x_api_token"

site:github.com ext:php "x-access-token"

site:github.com ext:php "x_access_token"

*\# GitLab repositories*

site:gitlab.com ext:php "api-key"

**Copied!**

[**AWS**](https://exploit-notes.hdks.org/exploit/reconnaissance/find-leaked-api-keys/#aws)

site:github.com ext:py "ap-northeast-1.amazonaws.com" "x-api-key"

**Copied!**

[**Google APIs**](https://exploit-notes.hdks.org/exploit/reconnaissance/find-leaked-api-keys/#google-apis)

site:github.com ext:py "googleapis.com" "?key="

**Copied!**

[**Hugging Face**](https://exploit-notes.hdks.org/exploit/reconnaissance/find-leaked-api-keys/#hugging-face)

site:github.com ext:py "https://api-inference.huggingface.co/models" "Authorization: Bearer"

**Copied!**

[**OpenAI**](https://exploit-notes.hdks.org/exploit/reconnaissance/find-leaked-api-keys/#openai)

site:github.com ext:py "https://api.openai.com/v1/models" "Authorization: Bearer"
