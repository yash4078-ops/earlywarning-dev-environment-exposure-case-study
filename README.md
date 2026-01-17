# earlywarning-dev-environment-exposure-case-study
Case study documenting public development and preview environment exposure findings, triage outcome, and security impact analysis from a responsible disclosure report.
# Exposed Development & Preview Environments – Case Study (Early Warning)

## Overview
This repository documents a real-world security assessment case study involving publicly accessible development and preview environments.  
The purpose of this case study is educational: to explain **why certain findings appear risky during reconnaissance but may be classified as non-impactful in bug bounty programs without exploit chaining**.

This report was responsibly disclosed via HackerOne and ultimately closed as *Informative* after triage review.

---

## Scope
- Organization: Early Warning
- Assets Tested:
  - zelle-fi-dev-qa.earlywarning.com
  - ssopreview.earlywarning.com
- Testing Type: Black-box, unauthenticated
- Disclosure Platform: HackerOne

---

## Observations

### 1. Publicly Accessible Dev / QA Environment
- A non-production environment was reachable without authentication
- Status/health information was visible
- No sensitive user data or administrative interfaces were exposed

### 2. Public Okta SSO Preview
- Okta preview login page accessible publicly
- No authentication bypass or misconfiguration identified
- No token leakage or auth flow weakness observed

### 3. CSP Header Information Disclosure
- Content-Security-Policy headers exposed internal Salesforce sandbox domains
- Example patterns:
  - `*.sandbox.my.salesforce.com`
  - internal dev naming conventions

---

## Security Analysis

While the exposure appeared concerning during reconnaissance, further analysis confirmed:

- No authentication bypass
- No access to sensitive data
- No production system interaction
- No credential, token, or API key leakage
- No privilege escalation or lateral movement

The exposed information remained **contextual and non-exploitable**.

---

## Disclosure Outcome
The report was reviewed and closed as **Informative** because:

- Development and preview environments may be intentionally public
- CSP header values alone do not constitute a vulnerability
- No practical exploitation scenario was demonstrated
- No measurable security impact on production systems

This outcome aligns with standard bug bounty triage guidelines.

---

## Key Learnings

- Public dev environments are not vulnerabilities by default
- Information disclosure requires *exploitation context* to be valid
- Reconnaissance findings must be chained to impact
- CSP leaks without sensitive tokens are informational
- Bug bounty programs prioritize demonstrated risk over theoretical risk

---

## What Would Have Made This Valid
This finding could have escalated if any of the following were present:

- Hardcoded credentials or secrets
- Authentication bypass
- Token or session leakage
- Dev → prod access pivot
- Misconfigured Okta flows (redirect_uri, MFA bypass)
- Sensitive API exposure

---

## Purpose of This Repository
This case study is shared to help:

- Junior researchers understand triage decisions
- Security teams evaluate recon vs impact
- Researchers improve report quality and exploit chaining

---

## Disclaimer
This repository is for educational and defensive research purposes only.

- No systems were harmed
- No data was accessed or misused
- No confidential information is disclosed
- All testing followed responsible disclosure practices

---

## Author
Sachin Mishra  
Independent Security Researcher  
Bug Bounty · Web Security · Recon & Analysis
