# swiss-bug-bounty-program

We, Swisscom Ltd and our affiliated companies (hereinafter "Swisscom") aim to design and operate our products and services according to the highest security standards to keep our customers safe. To this end, we are continually improving our security on multiple levels. We are aware that, despite all efforts, absolute security is impossible, and we cannot completely rule out the existence of security bugs. The purpose of the Swisscom Vulnerability Disclosure Policy and Bug Bounty Programme is to support the reporting of potential vulnerabilities in our systems by external parties.

Customers, users, researchers, partners and any other parties who interact with Swisscom's products and services are encouraged to report identified vulnerabilities to our security team under observance of our Responsible Disclosure Policy.

Moreover, we invite both private individuals and legal entities to participate in our Bug Bounty Programme (hereinafter the "Programme") in accordance with the Programme Rules. Bounties may be awarded for reporting qualifying and in-scope vulnerabilities.

Swisscom acknowledges the value of contributions from the security researcher community and highly appreciates the efforts made by the reporting party. We thank you in advance for your contribution!

TL;DR Swisscom Bug Bounty

Public programme  

Vulnerabilities
Qualifying Vulnerabilities
Any design, implementation or configuration issue that substantially affects confidentiality or integrity is likely to be eligible for a reward. Common examples include:

Remote code execution (RCE)
Code injections (HTML, JS, SQL, PHP, etc)
Cross-site scripting (XSS)
Horizontal and vertical privilege escalation
Broken authentication and session management
Sensitive data exposure
Denial-of-Service attacks 
# BUG BOUNTY — QUALIFYING VULNERABILITY CHECKLIST

## 🎯 CORE RULE

> **DO NOT REPORT A THEORETICAL WEAKNESS.**
>
> A finding should qualify only when you can demonstrate:
>
> **Vulnerability → Exploitation → Concrete Security Impact**

If there is no meaningful impact, classify it as:
`NOT QUALIFYING / INFORMATIONAL / DO NOT REPORT`

---

# ✅ QUALIFYING VULNERABILITIES

## 01 | Authentication Bypass

* [ ] Bypass login without valid credentials
* [ ] Access authenticated functionality without authentication
* [ ] Authentication logic bypass
* [ ] MFA bypass
* [ ] Password-reset authentication bypass
* [ ] OAuth/OIDC authentication bypass
* [ ] JWT authentication bypass
* [ ] Session authentication bypass

**Required:** Demonstrate unauthorised access to protected functionality/data.

---

## 02 | Authorisation / IDOR / BOLA

* [ ] Read another user's private data
* [ ] Modify another user's data
* [ ] Delete another user's data
* [ ] Access another organisation/tenant
* [ ] Privilege escalation
* [ ] Horizontal privilege escalation
* [ ] Vertical privilege escalation

**Required:** Use test accounts/data where possible and demonstrate actual cross-user or cross-tenant access.

---

## 03 | Account Takeover

* [ ] Password-reset takeover
* [ ] Email-change takeover
* [ ] MFA bypass leading to takeover
* [ ] OAuth account-linking takeover
* [ ] Session/token theft leading to takeover
* [ ] Authentication-flow manipulation

**Impact:** Ability to control or authenticate as another test/user account.

---

## 04 | SQL Injection

* [ ] Confirmed SQL injection
* [ ] Boolean-based SQLi
* [ ] Time-based SQLi
* [ ] Error-based SQLi
* [ ] UNION-based SQLi

**Required:** Demonstrate reliable database interaction without destructive actions.

---

## 05 | XSS

* [ ] Stored XSS
* [ ] Reflected XSS with meaningful impact
* [ ] DOM XSS
* [ ] XSS affecting another user's/browser context

**Do not report:** Self-XSS with no further impact.

---

## 06 | SSRF

* [ ] Server makes attacker-controlled request
* [ ] Internal service access demonstrated
* [ ] Cloud metadata access where explicitly authorised
* [ ] Internal endpoint/data access
* [ ] SSRF leading to credential/token disclosure

**Required:** Demonstrate meaningful server-side impact.
Do not access unrelated private data.

---

## 07 | Remote Code Execution

* [ ] Confirmed arbitrary code execution
* [ ] Command injection
* [ ] Template injection leading to execution
* [ ] Deserialisation leading to execution
* [ ] File-upload-to-code-execution

---

## 08 | File / Path Traversal

* [ ] Read sensitive server-side files
* [ ] Access files outside intended directory
* [ ] Arbitrary file access
* [ ] File overwrite with demonstrated security impact

**Required:** Use harmless proof files/targets where possible.

---

## 09 | Sensitive Information Disclosure

Qualifying only when the disclosed information has meaningful security impact:

* [ ] API secret allowing authenticated access
* [ ] Private authentication token
* [ ] Cloud credential
* [ ] Database credential
* [ ] Signing/private key
* [ ] Session token
* [ ] Sensitive internal data
* [ ] Confidential customer information

**DO NOT REPORT AS HIGH/MEDIUM merely because:**

* [ ] Server/version information is exposed
* [ ] Internal hostname is exposed
* [ ] Technology stack is disclosed
* [ ] Non-sensitive configuration is exposed
* [ ] Source maps exist without sensitive information

---

## 10 | Security Misconfiguration With Demonstrated Impact

Potentially qualifying:

* [ ] Public cloud bucket → sensitive data access
* [ ] Exposed admin interface → unauthorised access
* [ ] Debug endpoint → sensitive information/credentials
* [ ] Exposed configuration → usable secret/credential
* [ ] CORS misconfiguration → authenticated sensitive data readable
* [ ] Backup exposure → sensitive application data
* [ ] Open management interface → unauthorised control

**Rule:**

`Misconfiguration alone ≠ bounty`

`Misconfiguration + demonstrated impact = potentially qualifying`

---

## 11 | CORS

* [ ] Arbitrary Origin accepted
* [ ] Credentials accepted
* [ ] Victim authentication/session used
* [ ] Attacker-controlled origin can read sensitive response

**Strong evidence:**

`Attacker origin → victim authenticated request → sensitive response readable`

Wildcard CORS by itself is not automatically a vulnerability.

---

## 12 | CSRF

* [ ] State-changing action can be triggered cross-origin
* [ ] Victim authentication is automatically included
* [ ] Meaningful action occurs

Examples:

* [ ] Change email
* [ ] Change password
* [ ] Change MFA
* [ ] Add payment method
* [ ] Transfer funds
* [ ] Change security settings

---

## 13 | OAuth / OIDC

* [ ] Account takeover
* [ ] Token leakage
* [ ] Token substitution
* [ ] Improper redirect handling with meaningful impact
* [ ] Account-linking flaw
* [ ] Scope escalation
* [ ] Authentication bypass

---

## 14 | JWT / Session Security

* [ ] Authentication bypass
* [ ] Token forgery
* [ ] Algorithm confusion leading to access
* [ ] Session fixation with meaningful impact
* [ ] Session theft
* [ ] Cross-account session access
* [ ] Token privilege escalation

---

# 🔥 BRUTE-FORCE / AUTOMATED TESTING

## RULES ALLOW

* [ ] Confirm brute-force testing is explicitly permitted
* [ ] Confirm automation/scanning is permitted
* [ ] Confirm rate limits/concurrency restrictions
* [ ] Stay within the programme's allowed request volume
* [ ] Use test accounts whenever possible
* [ ] Stop immediately if service instability occurs

### Permitted testing can include

* [ ] Authentication rate-limit validation
* [ ] Password-policy testing
* [ ] OTP rate-limit testing
* [ ] Account-lockout testing
* [ ] API authentication testing
* [ ] Automated endpoint discovery
* [ ] Fuzzing within programme limits
* [ ] Nuclei/templates where allowed
* [ ] FFUF/Dirsearch/Katana where allowed
* [ ] Burp automated testing where allowed

### IMPORTANT

**Missing rate limiting alone is NOT automatically qualifying.**

Qualifying evidence would require a meaningful consequence, such as:

`Missing protection → practical authentication attack → account compromise`

or another concrete impact accepted by the programme.

---

# 🤖 AI-ASSISTED SECURITY TESTING

AI may be used to automate analysis and prioritisation:

* [ ] Analyse JavaScript bundles
* [ ] Extract API endpoints
* [ ] Identify authentication flows
* [ ] Identify parameters
* [ ] Detect potential IDOR locations
* [ ] Analyse API schemas
* [ ] Correlate recon results
* [ ] Generate test cases
* [ ] Prioritise attack surface
* [ ] Analyse HTTP responses
* [ ] Compare authenticated/unauthenticated behaviour
* [ ] Review scanner findings
* [ ] Generate validation steps
* [ ] Draft reports

-

**AI finding ≠ confirmed vulnerability.**

Every AI-generated finding must be independently validated.

---

# 🧪 EXPLOITATION VALIDATION

For every suspected vulnerability:

### STEP 1 — Detect

`Potential vulnerability`

↓

### STEP 2 — Reproduce

`Reliable reproduction`

↓

### STEP 3 — Validate

`Controlled exploitation`

↓

### STEP 4 — Demonstrate impact

`What can an attacker actually achieve?`

↓

### STEP 5 — Check programme policy

`Is this explicitly eligible?`

↓

### STEP 6 — Report

Only if the evidence satisfies the programme's rules.

---

# ❌ GENERALLY NON-QUALIFYING

Do NOT automatically report:

* [ ] Missing HSTS
* [ ] Missing CSP
* [ ] Missing X-Content-Type-Options
* [ ] Missing Permissions-Policy
* [ ] Missing cookie flag alone
* [ ] Version disclosure
* [ ] Server banner disclosure
* [ ] Technology-stack disclosure
* [ ] Internal hostname disclosure without impact
* [ ] Open redirect without additional impact
* [ ] Self-XSS
* [ ] Rate-limit absence without impact
* [ ] Generic scanner output
* [ ] Theoretical SSRF
* [ ] Theoretical SQLi
* [ ] Theoretical IDOR
* [ ] Theoretical CORS
* [ ] HTTP available without demonstrated sensitive-data exposure
* [ ] Public login page
* [ ] robots.txt information alone
* [ ] Standard WordPress endpoints
* [ ] Public source maps without sensitive information
* [ ] Debug/version information without security consequence

---

# 🏆 REPORT-QUALITY CHECK

Before submitting, answer YES to these:

* [ ] Is the asset explicitly in scope?
* [ ] Is the vulnerability reproducible?
* [ ] Can I demonstrate exploitation?
* [ ] Is there concrete security impact?
* [ ] Can I explain the attacker threat model?
* [ ] Can I provide clean HTTP evidence?
* [ ] Can another researcher reproduce it?
* [ ] Does the programme accept this vulnerability class?
* [ ] Did I stay within testing rules?
* [ ] Did I avoid unnecessary private-data access?
* [ ] Did I avoid destructive testing?

##

note : accpted vulnerblity which is exploit not only therolical 


 Non-Qualifying Vulnerabilities ::
 The absence of a security feature alone without demonstrated impact
Missing security best practice
Disclosure of non-sensitive information, even in bulk
Denial-of-Service attacks
"Self" XSS without demonstration of further impact (e.g. no adverse effects on victim)

# The authoritative source of the program scope is located at 
https://github.com/jatinpatel-hacker33/swiss-bug-bounty-program/edit/main/README.md  
   
# Ajila AG
*.ajila.com
*.digital.deals


# Axept Business Software AG
*.adapt-solutions.ch
*.axept.ch
*.provis.ch
*.provisag.ch


# Blue Entertainment AG
*.blue-plus.ch
*.blue.ch
*.bluecinema.ch
*.bluenews.ch
*.blueplus.ch
*.kit.ag
*.kitag.com
*.kitagcinemas.ch
*.teleclub.ch
*.teleclubsport.ch

# comPlan
*.pk-complan.ch


# Global IP Action AG
*.globalipaction.ch
*.glipac.ch

# Innovative Web Marketing & Service AG
*.i-web.ch
*.i-web-status.ch

# JLS Digital AG
*.jls.ch
*.jls.digital


# MTF Solutions AG
api.mailarchiver.mtfcloud.ch
bgv.filecloud.mtfcloud.ch
filecloud.mtfcloud.ch
status.mtfcloud.ch
zabbix.mtf.li

# Swisscom (Schweiz) AG
*.079.ch
*.bluewin.ch
*.conextrade.com
*.curabill.ch
*.cura-med.ch
*.digitalassessment.ch
*.ealarm-safemode.ch
*.ealarmstarter.ch
*.ellb.ch
*.h-net.ch
*.hcard.ch
*.helloclass.ch
*.intswisscom.com
*.ip-plus.net
*.jlr-connect.ch
*.labnet.ch
*.mccip.ch
*.medicalconnector.ch
*.medicalexchange.ch
*.medicalshare.ch
*.mucc-services.ch
*.mycloud.ch
*.mycloudswisscom.ch
*.projectmm.ch
*.pwlan.ch
*.scbs.ch
*.scsstatic.ch
*.sctv.ch
*.securepop.ch
*.sinso.ch
*.smeoffer.ch
*.swisscloud.io
*.swisscom-alarm.ch
*.swisscom-flaechen.ch
*.swisscom-learningcenter.ch
*.swisscom-shop.ch
*.swisscom-tv.com
*.swisscomcloud.com
*.swisscom-mcc.ch
*.swisscom.ai
*.swisscom.ch
*.swisscom.com
*.swisscomras.ch
*.swissdigicert.ch
*.swisstrustcert.ch
*.swisstrustroom.ch
*.swisstrustroom.com
*.triamed.ch
*.volvo-online.ch
*.webtiser.ch
*.webtiser.com
*.wingo.ch
https://github.com/swisscom/

# Swisscom Broadcast AG
*.sbcdc.ch
*.swisscomcdn.ch

# Swisscom Digital Technology SA
*.owt.swiss

# Swisscom Directories AG
*.akupunkturvergleich.ch
*.apotheken-vergleich.ch
*.architektvergleich.ch
*.augenarztvergleich.ch
*.bestattungsvergleich.ch
*.bijouterie-vergleich.ch
*.bodenlegervergleich.ch
*.bäckereivergleich.ch
*.cateringvergleich.ch
*.coaching-vergleich.ch
*.coiffeurvergleich.ch
*.consultingvergleich.ch
*.digitalone.ch
*.directories.ch
*.directoriesdata.ch
*.druckereien-vergleich.ch
*.e-directories.ch
*.elektrikervergleich.ch
*.ernaehrungsberatungsvergleich.ch
*.etv.ch
*.fahrlehrervergleich.ch
*.fitnessstudio-vergleich.ch
*.floristvergleich.ch
*.fondue-vergleich.ch
*.fotografvergleich.ch
*.fotografvergleich.ch
*.garage-vergleich.ch
*.gartenbauvergleich.ch
*.gu-vergleich.ch
*.hautarztvergleich.ch
*.immoverwaltungsvergleich.ch
*.informatikervergleich.ch
*.innenarchitektvergleich.ch
*.kinderarztvergleich.ch
*.kinderkrippen-vergleich.ch
*.kmudigital.ch
*.kosmetikvergleich.ch
*.local.ch
*.localcities.ch
*.localclubs.ch
*.localina.com
*.localreservation.ch
*.localsearch-business.ch
*.localsearch-free.ch
*.localsearch-hosting.ch
*.localsearch.ch
*.localsearch.tech
*.localsearchweb.ch
*.maler-gipser-vergleich.ch
*.massagevergleich.ch
*.metzgereivergleich.ch
*.multisource.ch
*.multisourcepro.ch
*.mycommerce.shop
*.mylocalina.ch
*.nachhilfevergleich.ch
*.nagelstudiovergleich.ch
*.oeffentliches-verzeichnis.ch
*.optiker-vergleich.ch
*.osteopathievergleich.ch
*.pannenhilfevergleich.ch
*.pflegeheimvergleich.ch
*.physiotherapievergleich.ch
*.public-directory.ch
*.reinigungsfirmavergleich.ch
*.reisebuerovergleich.ch
*.renovero.ch
*.sanitaervergleich.ch
*.scdag.net
*.schreinervergleich.ch
*.search.ch
*.sospos.ch
*.swisslist.ch
*.tanzschulvergleich.ch
*.tennisclubvergleich.ch
*.tierarztvergleich.ch
*.umzugsfirma-vergleich.ch
*.veloshop-vergleich.ch
*.wellness-spa-vergleich.ch
*.websheep.com
*.yoga-pilates-vergleich.ch

# Swisscom Event & Media Solutions AG
*.swisscomstream.ch
*.truvami.com
*.veertly.ch
*.veertly.de

# Swisscom Secure Vision AG
*.audiovideo-sa.ch
*.crowdinsider.ch
*.viaas.ch
*.videoinsider.ch

# Teldas GmbH
*.teldas.ch
www.numberportability.ch
ws.numberportability.ch
testsrv.numberportability.ch
ws.testsrv.numberportability.ch

# United Security Providers AG
*.u-s-p.ch
*.united-security-providers.ch

# Worklink AG
*.worklink.ch

# cablex AG
*.cablex.ch
*.cablex-toolbox.ch
*.mycablex.ch

# itnetX (Switzerland) AG
*.itnetx.ch
