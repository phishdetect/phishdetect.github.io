# Threat Model

This document outlines the threat model for PhishDetect's architecture and its various software component. This document is inspired by [SecureDrop's threat model](https://docs.securedrop.org/en/stable/threat_model/threat_model.html). Because PhishDetect is under active development, this document is always a work in progress.

## Trust Levels

PhishDetect Node currently supports three user trust levels **user**, **submitter** and **admin**, which are respectively assigned the numerical values **0**, **1** and **2**. These values are used to evaluate whether a client has sufficient permissions to access a given API route. For more information about PhishDetect Node's REST API and its routes' permission levels please read [here](/api/rest.md).

In this section we explain the general capabilities we expect the three trust levels to access.

### User
- Fetch the list of indicators only in hashed form.
- Automatically submit "*alerts*" of suspicious events. Alerts should only contain metadata (email addresses, URLs) and no content (full-source emails, content at URL).
- Manually submit "*reports*" of suspicious emails and websites. Reports can contain content, typically only in the case of full-source emails.
- Submit requests of "*reviews*" of websites which might have been mistakenly blocked.
- Request the static analysis of a domain or a URL, if the PhishDetect Node enables analysis.
- Request the static analysis of HTML pages, if the PhishDetect Node enables analysis.
- Request the dynamic analysis of URLs, if the PhishDetect Node enables analysis.

### Submitter
- All of the above.
- Add new indicators to PhishDetect Node.

### Administrator
- All of the above.
- Enable or disable indicators on PhishDetect Node.
- Retrieve details of hashed indicators (including the clear-text original).
- Add, activate, and deactivate users of PhishDetect Node.
- Inspect "*alerts*" submitted to PhishDetect Node.
- Inspect "*reports*" submitted to PhishDetect Node.
- Inspect "*reviews*" requests submitted to PhishDetect Node.

---

## Implications

### What a Compromise of PhishDetect Node Can Surrender
- If a PhishDetect Node is compromised, the attacker can inspect all registered users, retrieve their registration details including name, email address/contact details and API keys. The attacker could impersonate or deactivate existing users, and add an activate new users.
- Depending on the configuration of the webserver running PhishDetect Node, if compromised, the attacker could gain additional insights on users and any logged activity, including for example the IP address and the date and time of requests made to the server.
- If a PhishDetect Node is compromised, the attacker can inspect all indicators stored in clear-text and served to users.
- If a PhishDetect Node is compromised, the attacker can add new indicators for clients to download, and potentially cause (temporary) disruption against particular services.
- If a PhishDetect Node is compromised, the attacker can inspect all full-source emails and links reported by users.
- If a PhishDetect Node is compromised, the attacker can inspect all indicators users requested to be reviewed.
- If a PhishDetect Node is compromised, the attacker could find ways to deliver malformed data to cause, for example, Cross-Site Scripting or other injection attacks on PhishDetect Browser Extension users.

### What a Compromise of PhishDetect Browser Extension Can Surrender

### What a Malicious Website Visited by PhishDetect Browser Extension Can Surrender

### What a Malicious Website Analyzed by PhishDetect Node Can Surrender

### What a Compromise of Add-On Store Packages Can Surrender
- Through the compromise of the account associated with Add-On Stores the attackers can upload malicious updates to PhishDetect Browser Extension which could result in the compromise of PhishDetect users.

### What the Compromise of the PhishDetect Admin Utility Can Surrender

### What a Generic Motivated Attacker Can Achieve
- A Generic Motivated Attacker can attempt to launch a Distributed Denial of Service attack against the PhishDetect Node.
- If the PhishDetect Node offers analysis, and particularly without authentication of vetted users, a Generic Motivated Attacker can overload the PhishDetect Node by flooding it with requests to dynamically analyze a link.
- If the PhishDetect Node does not enforce authentication of vetted users, a Generic Motivated Attacker can pollute the database with bogus alerts, reports, and reviews requests.
- If the PhishDetect Node does not enforce authentication of vetted users, a Generic Motivated Attacker can retrieve the list of hashed indicators and attempt to enumerate which websites or email addresses are blocklisted by the Node operators.
- If the PhishDetect Node does not enforce authentication of vetted users, a Generic Motivated Attacker can attempt to submit specially crafted "alerts", "reports" and "reviews" to execute NoSQL injections.
- If the PhishDetect Node does not enforce authentication of vetted users, a Generic Motivated Attacker can attempt to submit specially crafted "alerts", "reports" and "reviews" to execute Cross-Site Scripting on a PhishDetect Admin interface.

### What a Local Network Attacker Can Achieve Against User, Submitter or Administrator
- A Local Network Attacker can observe if a User, Submitter or Administrator is accessing a particular PhishDetect Node.
- A Local Network Attacker can prevent a User, Submitter or Administrator from accessing a PhishDetect Node.

### What a Nation-wide Network Adversary Can Achieve Against User, Submitter or Administrator
- A Nation-wide Network Adversary can observe if any User, Submitter or Administrator in a country is accessing a particular PhishDetect Node through DNS or IP protocols inspection.
- A Nation-wide Network Adversary can block access to a PhishDetect Node to any or all Users, Submitters or Administrators.
- A Nation-wide Network Adversary capable of forging valid TLS certificates might be able to intercept any transmission from Users, Submitters or Administrators to a PhishDetect Node.
