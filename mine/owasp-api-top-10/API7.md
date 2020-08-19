# API7:2019
---
## Security Misconfiguration

-----

## Security Misconfiguration

> Security misconfiguration is commonly a result of unsecure default configurations, incomplete or ad-hoc configurations, open cloud storage, misconfigured HTTP headers, unnecessary HTTP methods, permissive Cross-Origin resource sharing (CORS), and verbose error messages containing sensitive information.

-----

## In other words...

- Missing / incorrect security hardening
- Overly permissive cloud service settings
- Missing or weak TLS
- No security headers, CORS policy
- Systems unpatched
- Sensitive info exposed
  - Error messages with stack traces

-----

## Implications

- Data exposure
- Potential: full server compromise

-----

## Example: `HTTP TRACE` verb

- `HTTP TRACE` returns entire HTTP request
  - Includes headers like `Authorization`
- Pairs excellently with cross-site scripting (XSS)
  - Attackers can steal authZ header value

-----

## Just ask Equifax...
#### May - July 2017

CVE-2017-5638 - Apache Struts2 S2-045

> It is possible to perform a RCE attack with a malicious `Content-Type` value. If the `Content-Type` value isn't valid an exception is thrown which is then used to display an error message to a user.

Jakarta Multiparser attempts to include `Content-Type` value in message, accidentally parses and executes code.
- Fixed March 7
- Actively exploited by March 10

https://cwiki.apache.org/confluence/display/WW/S2-045

-----

## Just ask Equifax...
#### May - July 2017

- May 12: exploited on credit dispute website
- July 29: discovered by Equifax
- July 30: fixed & deployed


Impact
- 147.9 million American consumer records accessed
- 10-11 million drivers' licenses

-----

## Just ask Github...
#### June 2019

Abused Rails default `HTTP HEAD` behavior
- If unhandled, routes to `HTTP GET` endpoint

```
# In the router

match "/login/oauth/authorize", # For every request with this path...
  :to => "[the controller]", # ...send it to the controller...
  :via => [:get, :post] # ... as long as it's a GET or a POST request.
```
```
# In the controller

if request.get?
  # serve authorization page HTML
else
  # grant permissions to app
end
```

https://blog.teddykatz.com/2019/11/05/github-oauth-bypass.html

-----

## Prevention

- Environment hardening process
  - Automate creating a secure environment
- Review configurations across entire stack
  - Deploy scripts, app server settings, cloud services
- Always use TLS
- Disable unused verbs
- Configure security headers
  - CORS, Strict Transport Security (HSTS), Content Security Policy