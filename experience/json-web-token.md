# JSON Web Token

## Use cases

* When needs to verify approval to third party components.
* When needs to generate time expiring access control related token.
* When verification of payload in required.

## Overview

JWT consists in 3 parts, and joined in dots, i.e.:

`<Encoded Header>.<Encoded Payload>.<Signature>`

### Header

Mostly indicates the token type\(i.e. `JWT`\), and signing algorithm\(e.g. `HS256`\). i.e.:

```javascript
{
  "alg": "HS256",
  "typ": "JWT"
}
```

Then the JSON is **Base64Url** encoded

### Payload

**Base64Url** encoded JSON string which marked the message wanted to transfer.

Conventions: [IANA JSON Web Token Registry](https://www.iana.org/assignments/jwt/jwt.xhtml)

### Signature

Depends on the signing algorithm, but `<Encoded Header>.<Encoded Payload>` and `secret` will be included

## Signing Algorithm

[General List](https://tools.ietf.org/html/rfc7518#section-3)

### Algorithm names convention

| Series | Meaning |
| :--- | :---: |
| HSxxx | HMAC is used. Uses same secret for verification. |
| RSxxx | RSA is used. Uses key pair for verification.\(e.g. SSH key pair\) |
| ESxxx | ECDSA is used. Uses key pair for verification. |

## Reference

[https://jwt.io/](https://jwt.io/)

[https://tools.ietf.org/html/rfc7519](https://tools.ietf.org/html/rfc7519)

