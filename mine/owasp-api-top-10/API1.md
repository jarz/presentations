# API1:2019
---
## Broken Object Level Authorization

-----

## Broken Object Level Authorization

> APIs tend to expose endpoints that handle object identifiers, creating a wide attack surface Level Access Control issue.

> Object level authorization checks should be considered in every function that accesses a data source using an input from the user.

-----

## In other words...

- Most API endpoints use IDs in requests
  - `GET /api/users/tim`
- It's easy to simply swap IDs in a request
  - `GET /api/users/tim` => `GET /api/users/admin`
- Particularly bad when IDs easily enumerated
  - `GET /api/users/1`, `GET /api/users/2` ...
- Most common API vulnerability

-----

## Implications

- Unauthorized data access
  - _"Yet another website loses your data, story at 10."_
- Unauthorized data modification
  - Account take-over

-----

## Just ask Uber...
#### April 2019

Found by Anand Prakash @ AppSecure

https://appsecure.security/blog/how-i-could-have-hacked-your-uber-account

-----

#### Just ask Uber...

Two endpoints expose user UUIDs (first)

<table>
<tbody>
  <tr>
    <td><pre><code>POST /p3/fleet-manager/\_rpc?rpc=addDriverV2 HTTP/1.1
Host: partners.uber.com
{"nationalPhoneNumber":"99999xxxxx","countryCode":"1"}</code></pre></td>
  </tr>
  <tr>
    <td><pre><code>{
  "status":"failure",
  "data": {
    "code":1009,
    "message":"Driver '47d063f8–0xx5e-xxxxx-b01a-xxxx' not found"
  }
}</code></pre></td>
  </tr>
</tbody>
</table>

-----

#### Just ask Uber...

One endpoint exposes user UUIDs (second)

<table>
<tbody>
  <tr>
    <td><pre><code>POST /p3/fleet-manager/\_rpc?rpc=addDriverV2 HTTP/1.1
Host: partners.uber.com
{"email":"xxx@gmail.com"}</code></pre></td>
  </tr>
  <tr>
    <td><pre><code>{
  "status":"failure",
  "data": {
    "code":1009,
    "message":"Driver 'ca111b95–1111–4396-b907–83abxxx5f7371e' not found"
  }
}</code></pre></td>
  </tr>
</tbody>
</table>

-----

## Just ask Facebook...
#### June 2015

Delete any user's notes

```
POST /a/note.php?note_id=[victim’s note id]&publish&gfid=[attacker’s token]
Host: touch.facebook.com

fb_dtsg=[attacker’s token]&charset_test=&title=&body=&privacy=&=Publish&_dyn=&__user=[attacker’s userID]
```

https://web.archive.org/web/20190215144609/http://www.anandpraka.sh/2015/12/summary-this-blog-post-is-about.html


-----

## Prevention

- Implement a robust authorization mechanism
  - Straighforward, based on user type
  - Complex, based on role assignment

- **Always use** that authorization mechanism validate user-resource access
  - Secure by default: configure middleware
  - Check authorization through the entire stack _(including the database!)_ <!-- Just an extra `AND` in a `WHERE` clause -->

-----

## Prevention

- Reduce exposure through GUIDs or other IDs
  - _Security through obscurity_, but every little bit helps! <!-- This could be a useful metric -->
  - Extra credit: log attempts, detect brute-force attacks

- **Test** your authorization code automatically through unit _and_ integration tests
  - It's great that your auth has 100% test coverage...
  - But what if it's not configured correctly?