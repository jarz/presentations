# API4:2019
---
## Lack of Resources & Rate Limiting

-----

## Lack of Resources & Rate Limiting

> Quite often, APIs do not impose any restrictions on the size or number of resources that can be requested by the client/user. Not only can this impact the API server performance, leading to Denial of Service (DoS), but also leaves the door open to authentication flaws such as brute force.

-----

## In other words...

- Most developers don't think about rate limiting, etc.
- This leaves APIs vulnerable to attacks
  - Denial of Service
  - Brute-force

-----

## Implications

- Downtime
- Account compromise
- Eroded trust

-----

## Just ask Facebook...
#### February 2016

- Rate limits on password reset
  - 6 digit code sent via SMS
  - ... except beta environment
- Able to brute force code

https://www.youtube.com/watch?v=U3Of-jF1nWo

-----

## Just ask Stack Overflow...
#### July 2016

ReDoS: Regex-based Denial of Service
- `^[\s\u200c]+|[\s\u200c]+$`: trim beginning and ending spaces
- Not awesome when a line is `--` followed by 20000 spaces
  - Checks 20,000+19,999+19,998+…+3+2+1 = 199,990,000 times

> This regular expression has been replaced with a substring function.

https://stackstatus.net/post/147710624694/outage-postmortem-july-20-2016

<!-- https://vimeo.com/112065252 -->

-----

## Prevention

- Implement client request rate limiting <!-- No RFC... -->
  - `HTTP 429 Too Many Requests`
  - Inform clients of rate limits
- Place global limits on requests
  - `Content-Length` header
- Identify ways to limit system resource usage <!-- Docker -->
