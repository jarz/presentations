# API2:2019
---
## Broken User Authentication

-----

## Broken User Authentication

> Authentication mechanisms are often implemented incorrectly, allowing attackers to compromise authentication tokens or to exploit implementation flaws to assume other user’s identities temporarily or permanently. Compromising system’s ability to identify the client/user, compromises API security overall.

-----

## Detour: Auth*N*&nbsp; vs Auth*Z*

https://www.okta.com/identity-101/authentication-vs-authorization/

-----

## Authentication
### (AuthN)

> Authentication is the act of validating that users are who they claim to be.

*Who* are you?
- Username
- Password
- SMS
- Smart card, Yubikey

-----

## Authorization
### (AuthZ)

> Authorization in system security is the process of giving the user permission to access a specific resource or function.

*What* can you do?
- Depends on each API
- Based on
  - Individual user
  - Group

-----

## Example: House-sitting
#### From Okta

### Authentication
- Unlock door with keys
  - _Granted access based on key possession_

---

### Authorization
- Feed the cats
  - _Given permission to go in pantry, etc._
- ~~Watch pay-per-view movies, host backyard bonfire~~
  - **No permission**

-----

### _Back to OWASP API2:2019..._

-----

## Broken User Authentication

> Authentication mechanisms are often implemented incorrectly, allowing attackers to compromise authentication tokens or to exploit implementation flaws to assume other user’s identities temporarily or permanently. Compromising system’s ability to identify the client/user, compromises API security overall.

-----

## In other words...
### Implementation

- Exposes sensitive authN details
  - Auth tokens in URLs
- Doesn't validate tokens
  - Signature, expiration
- Doesn't properly secure passwords
  - No / weak hashing
- Altogether wrong authN mechanism
  - Basic instead of per-app keys

-----

## In other words...
### Endpoint protection

- All authN endpoints have to be extra secure
  - Forgot Password / Account Recovery
  - One-click deep links in emails
- Brute force attacks
- Credential stuffing
  - Usernames and passwords leaked by other sites

-----

## Implications

- Unauthorized account access
  - Read / send messages
  - Buy things
  - Access personal data

-----

## Just ask Auth0
#### July 2019

> A lone path of one of our older, stable versions of our codebase was not using our standard baseline JWT implementation, which allowed a case-insensitive JWS algorithm to match an "unsigned" verifier. This affected a very small subset of our endpoints.

https://auth0.com/blog/insomnia-security-disclosure/

--- 

> The Authentication API prevented the use of `alg: none` with a case sensitive filter. This means that simply capitalising any letter e.g. `alg: nonE`, allowed tokens to be forged. 

https://insomniasec.com/blog/auth0-jwt-validation-bypass

-----

## Just ask Apple
#### May 2020

Sign in with Apple

```
POST /XXXX/XXXX HTTP/1.1
Host: appleid.apple.com

{"email":"contact@bhavukjain.com"}
```
---
```
{
  "authorization" : {
    "id_token" : "eyJraWQiOiJlWGF1bm1MIiwiYWxnIjoiUlMyNTYifQ.XXXXX.XXXXX",
    "grant_code" : "XXX.0.nzr.XXXX",
    "scope" : [ "name", "email" ]
  },
  "authorizedData" : {
    "userId" : "XXX.XXXXX.XXXX"
  },
  "consentRequired" : false
}
```
Valid `id_token` for any user

-----

## This stuff is hard

- Not even specialists get it right 100%...
- Consider using specialists
  - Resources
  - Research
  - CYA <!-- Assets -->

<!-- Would working on this spark joy? -->

-----

## Prevention

- Know your API's authN flows
  - Double-check with other devs
- Learn different authN standards
  - Not authN: OAuth
  - Yet authN: OpenID
- Use those standards!

-----

## Prevention

- Implement brute-force mitigations on authN endpoints
  - Rate-limiting, captcha, account lockout
- Protect accounts via MFA
  - Extra layer against credential stuffing