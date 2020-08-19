# API10:2019
---
## Insufficient Logging & Monitoring

-----

## Insufficient Logging & Monitoring

> Insufficient logging and monitoring, coupled with missing or ineffective integration with incident response, allows attackers to further attack systems, maintain persistence, pivot to more systems to tamper with, extract, or destroy data. Most breach studies demonstrate the time to detect a breach is over 200 days, typically detected by external parties rather than internal processes or monitoring.

-----

## In other words...

- Not logging enough
  - Code
  - Configuration
- Not monitoring
  - Logs
  - Infrastructure

-----

## Implications

- Lots of time to find, exploit vulnerabilities
- No idea of scope of compromise

-----

## Just ask Venmo
#### June 2019

> A computer science student has scraped seven million Venmo transactions to prove that users’ public activity can still be easily obtained, a year after a privacy researcher downloaded hundreds of millions of Venmo transactions in a similar feat.

https://venmo.com/api/v5/public
- Still accessible
- No auth

https://techcrunch.com/2019/06/16/millions-venmo-transactions-scraped/

-----

## Just ask First Amarican Financial Corp.
#### May 2019

> He said anyone who knew the URL for a valid document at the Web site could view other documents just by modifying a single digit in the link.

Potentially 885 million files

> “The title insurance agency collects all kinds of documents from both the buyer and seller, including Social Security numbers, drivers licenses, account statements, and even internal corporate documents if you’re a small business. You give them all kinds of private information and you expect that to stay private.”

No idea who's accessed what

https://krebsonsecurity.com/2019/05/first-american-financial-corp-leaked-hundreds-of-millions-of-title-insurance-records/

-----

## Prevention

- More logging!
  - Failed auth, access
  - Input validation errors
- Better logging!
  - Structured
  - Detailed (enough)
- Monitor logs!
  - SIEM systems, other aggregators <!-- firewall, application, rate limiting combined -->
  - Dashboards & alerts
