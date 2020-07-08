---
layout: post
title: pycurl cannot access cloudflare hosting websites
categories:
  - Python
---

# Cloudflare - Pycurl Denial of service

## Issue

When using pycurl access cloudflare websites, response code will be 403 denied, but using curl command will access normally.

## Procedure

Response from pycurl contains following line:

```text
<p>The owner of this website has banned your access based on your browser's signature.</p>
```

After Googling, it indicates it's the User-Agent error.

After serval try-and-error about Cloudflare websites, when using User-Agent:PycURL series will trigger Cloudflare return 403.

## Solution

#### USERAGENT update

mock other agents' signature to bypass Cloudflare's checking:

```text
__curl = pycurl.Curl()
__curl.setopt(pycurl.USERAGENT, <other user agents>")
```

