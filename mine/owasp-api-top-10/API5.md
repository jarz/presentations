# API5:2019
---
## Broken Function Level Authorization

-----

## Broken Function Level Authorization

> Complex access control policies with different hierarchies, groups, and roles, and an unclear separation between administrative and regular functions, tend to lead to authorization flaws. By exploiting these issues, attackers gain access to other users’ resources and/or administrative functions.

-----

## In other words...

- Authorization code gets complicated
- Attackers exploit logic errors
- Attackers make informed guesses and get lucky
  - Change the verb from `GET` to `PUT`
  - Change the URL from `.../users/...` to `.../admins/...`

-----

## Implications

- Attackers access unauthorized functionality
  - Usually administrative
- System integrity is suspect   

-----

## Just ask New Relic...
#### August 2020

> Attacker can create new account inside any partnership with no approval from the partnership owner.

https://hackerone.com/reports/786109

-----

## Just ask Shopify...
#### September 2017

Bypass admin auth

> The code did not properly check what type the existing account was, and therefore an existing collaborator account in the "pending" state (not yet accepted by the store owner) would be converted into an active collaborator account, effectively allowing the partner to approve their own request without interaction from the store owner.

https://hackerone.com/reports/270981

-----

## Prevention

- Implement an API-wide authorization mechanism
  - Configure middleware, secure-by-default policy
  - Use on all controllers/actions
- Review endpoints for correct authorization levels
  - Regular users shouldn't be able to _???_
- Administrative functions should build in additional authorization checks
  - Defense-in-depth