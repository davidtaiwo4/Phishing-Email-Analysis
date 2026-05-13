# Phishing Email Analysis

## Overview

This project demonstrates the analysis of a phishing email designed to impersonate Banco Bradesco and Livelo reward services. The objective was to identify Indicators of Compromise (IOCs), analyze email headers, inspect sender infrastructure, and determine the malicious intent of the message.

The investigation involved email header analysis, URL inspection, sender verification, and phishing detection techniques commonly used in Security Operations Center (SOC) environments.

---

# Project Objectives

- Analyze raw phishing email headers
- Identify spoofed sender information
- Extract malicious URLs and IP addresses
- Investigate SPF, DKIM and DMARC results
- Detect social engineering techniques
- Document Indicators of Compromise (IOCs)
- Produce a threat analysis report

---

# Email Overview

Email Screenshot<img width="1866" height="791" alt="Screenshot 2026-05-12 220039" src="https://github.com/user-attachments/assets/9be8db2a-c87f-417f-8b61-86ba20c7ae3c" />

The phishing email impersonated Banco Bradesco (a financial institution in Latin America) and claimed that the recipient had reward points expiring on the same day in order to create urgency and encourage interaction.

#### Email translation:
Main Text (Top Section):

- You have Livelo Points with your Banco do Bradesco card available for redemption that expire TODAY; avoid losing these points by redeeming your Visa Infinite Score right now
- You (Banco do Bradesco Customers ) accumulate Livelo points every time you use your cards in the debit or credit function; it is quick and easy to accumulate.
  
Red Banner Section:

- Exchange your points for airline miles
- Discounts of up to 35% on your card bill
- 92,990 THOUSAND ACCUMULATED POINTS EXPIRE TODAY
  
Call to Action:
- Button: Redeem Now
- Bottom Text: Redeem right now before they expire! Take advantage, Exchange your points for airline miles, Discounts of up to 35% on your card or thousands of prizes in our Catalog.

#### Suspicious Characteristics
- Fake banking branding
- Urgent language
- Suspicious sender infrastructure
- Embedded links

---

## Phishing Email Analysis


### Step 1 — Header Analysis

Email header <img width="1077" height="370" alt="Screenshot 2026-05-12 2201552" src="https://github.com/user-attachments/assets/eab1c333-bf4c-49e5-90b3-ed32fbaec4d3" />


The email headers were analyzed to trace the true origin of the message and verify sender authenticity.

Analysis of the email header using google message header <img width="1279" height="840" alt="Screenshot 2026-05-12 224026" src="https://github.com/user-attachments/assets/fc522543-d519-4ca9-b6dc-e2c8b25c8b49" />

Email header analysis with Azure message header analyzer <img width="1892" height="877" alt="Screenshot 2026-05-12 230904" src="https://github.com/user-attachments/assets/d36f7523-b770-4883-9c2e-14e83da277f6" />



### Findings
- The email originated from a suspicious VPS server
- SPF validation failed
- DKIM signature was missing
- DMARC authentication failed
- The sender domain did not match legitimate banking infrastructure
- The displayed sender attempted to impersonate Banco Bradesco using deceptive naming conventions.
- Embedded link.


### Key Indicators
- Sender IP Address: `137.184.34.4`
- Suspicious Return Path
- Suspicious link -https://blog1seguimentmydomaine2bra[.]me/ (defanged)


---

### Step 2 — Sender Verification


### Displayed Sender
- `BANCO DO BRADESCO LIVELO` banco.bradesco@atendimento.com.br

### Actual Infrastructure
- Non-corporate mail server
- Suspicious domain usage

This mismatch strongly indicated sender spoofing and phishing activity.


---

### Step 3 — URL & IP Analysis

Embedded links inside the email were inspected to determine whether they redirected users to malicious websites.

### Findings
- The URL did not belong to Banco Bradesco
- Domain naming attempted to mimic legitimate branding


### Suspicious Domain
- `blog1seguimentmydomaine2bra.me`

---

###  Malicious Link Analysis

Embedded link was analysed with VirusTotal <img width="1885" height="870" alt="Screenshot 2026-05-12 232911" src="https://github.com/user-attachments/assets/35b25fcd-1009-4445-9c6b-e7633e676aaa" />

The suspicious link was opened in a browser sandbox (Browserling) <img width="1474" height="908" alt="Screenshot 2026-05-13 133524" src="https://github.com/user-attachments/assets/3f542d14-6dbe-447d-93c2-9c697131d8f1" />

## IP Analysis

Sender Ip Reputation with ip2location <img width="1830" height="876" alt="Screenshot 2026-05-13 153552" src="https://github.com/user-attachments/assets/f31baecc-558f-4d0e-97ee-9ac6e6388b31" />


---

### Step 4 — Social Engineering Analysis

The phishing email used psychological manipulation techniques to pressure the victim into clicking the malicious link.

### Techniques Observed
- Urgency (“points expiring today”)
- Fear of losing rewards
- Fake financial incentives
- Trust impersonation using banking logos and branding

These are common phishing tactics used to increase click rates.

---

##  Phishing Email Body

Phishing Email Body <img width="831" height="555" alt="Screenshot 2026-05-13 150748" src="https://github.com/user-attachments/assets/01366898-3666-41a1-867a-383bb4d1088b" />

---

### Step 5 — IOC Extraction

Indicators of Compromise (IOCs) were extracted from the email for threat hunting and future detection activities.

### Extracted IOCs

| IOC Type | Value |
|---|---|
| IP Address | `137.184.34.4` |
| Malicious Domain | `blog1seguimentmydomaine2bra.me` |
| Fake Sender Email | `banco.bradesco@atendimento.com.br` |
| Subject Line | `Seu cartão tem 92.990 pontos LIVELO expirando hoje!` |


---

### Step 6 — Threat Assessment

Based on the findings, the email was classified as a phishing attempt with a probability of credential theft.

### Threat Indicators
- Spoofed sender identity
- Suspicious hosting infrastructure
- Embedded links
- Social engineering tactics

### Risk Level
- high

---

# MITRE ATT&CK Mapping

| Technique | ID |
|---|---|
| Phishing | T1566 |
| Spearphishing Link | T1566.002 |
| Credential Harvesting | T1056 |
| Masquerading | T1036 |

---


---

## Email Investigation Report

### Incident Summary

| Field | Details |
|---|---|
| Incident Type | Suspected Phishing Email |
| Analysis Date | 19 September 2023 |
| Severity | Medium |
| Classification | Suspicious Email / Potential Phishing |
| Status | Closed – No Confirmed Malicious Activity |
| Delivery Method | Email |
| User Impact | No user interaction confirmed |

---

## Executive Summary

A suspicious email impersonating Banco Bradesco and Livelo rewards services was analyzed after being reported for potential phishing activity. The message used urgency-based social engineering techniques, claiming that reward points were expiring on the same day.

Initial analysis identified multiple phishing indicators including:
- Suspicious sender infrastructure
- SPF processing issues
- Missing DKIM signature
- Authentication failures
- External embedded link
- Banking impersonation

Threat intelligence and reputation checks were performed on the sender IP address and embedded URL. At the time of investigation, no known malicious or suspicious detections were identified for the IP address or domain in publicly available threat intelligence platforms.

Due to the lack of confirmed malicious detections, the incident could not be conclusively classified as confirmed phishing. However, based on the spoofing indicators and social engineering characteristics, the email was classified as a **Suspicious Email / Potential Phishing Attempt**.

---

### Email Metadata

| Field | Value |
|---|---|
| Subject | CLIENTE PRIME - BRADESCO LIVELO: Seu cartão tem 92.990 pontos LIVELO expirando hoje! |
| From | BANCO DO BRADESCO LIVELO <banco.bradesco@atendimento.com.br> |
| Reply-To | Not Present |
| Return-Path | root@ubuntu-s-1vcpu-1gb-35gb-intel-sfo3-06 |
| Recipient | phishing@pot |
| Date | Tue, 19 Sep 2023 18:35:49 +0000 |
| Content Type | text/html |
| Encoding | base64 |

---


### Authentication Results

| Security Control | Result |
|---|---|
| SPF | TempError |
| DKIM | None |
| DMARC | TempError |
| Composite Authentication | Fail |

### Observation

Authentication mechanisms either failed or were not properly configured. While this increases suspicion, SPF TempError alone is not sufficient evidence of malicious intent because DNS lookup timeouts can occur legitimately.

---

### Embedded Link Analysis

| Artifact Type | Value |
|---|---|
| URL | https://blog1seguimentmydomaine2bra.me/ |
| URL Reputation | No detection at time of analysis |
| Domain Category | Unclassified |
| HTTPS Enabled | Yes |

### Observation

The embedded domain used branding-related naming intended to resemble a legitimate financial or promotional service. However, threat intelligence checks did not return confirmed malicious detections during the investigation.

---

### Threat Intelligence Findings

##### IP Address Reputation

| IOC | Result |
|---|---|
| 137.184.34.4 | No malicious detections found |

## Domain Reputation

| IOC | Result |
|---|---|
| blog1seguimentmydomaine2bra.me | No malicious detections found |

### Threat Intelligence Sources Used

- VirusTotal
- URLScan
- IpInfo
- ip2location
- WHOIS review

### Observation

No active detections or blacklist entries were identified for the sender IP or embedded domain at the time of analysis.

---

### Social Engineering Indicators

The email displayed multiple characteristics commonly associated with phishing campaigns:

- Urgency-based messaging
- Financial incentive lure
- Banking impersonation
- Reward expiration warning
- External link redirection
- HTML formatted email with branding


### Indicators of Compromise (IOCs)

| IOC Type | Value |
|---|---|
| Sender IP | 137.184.34.4 |
| Domain | blog1seguimentmydomaine2bra.me |
| Return-Path | root@ubuntu-s-1vcpu-1gb-35gb-intel-sfo3-06 |
| Sender Email | banco.bradesco@atendimento.com.br |
| Subject | CLIENTE PRIME - BRADESCO LIVELO: Seu cartão tem 92.990 pontos LIVELO expirando hoje! |

---

### Analyst Assessment

## Classification Decision

| Classification | Result |
|---|---|
| Confirmed Phishing | No |
| Malicious Confirmed | No |
| Suspicious | Yes |
| False Positive | No |

### Final Assessment

The email contains multiple suspicious characteristics consistent with phishing activity; however, there was insufficient evidence to conclusively classify the message as confirmed malicious due to:

- No threat intelligence detections
- No confirmed payload delivery
- No confirmed credential harvesting activity
- No endpoint compromise identified

The incident is therefore classified as:

```text
Suspicious Email / Potential Phishing Attempt
```

---

## Recommended Actions

- Continue monitoring the sender IP and domain
- Block or quarantine similar messages if organizational policy requires
- Educate users on phishing indicators
- Add suspicious domain monitoring to SIEM tools
- Escalate if future detections or user compromise indicators appear

---

## MITRE ATT&CK Mapping

| Technique | ID |
|---|---|
| Phishing | T1566 |
| Spearphishing Link | T1566.002 |
| Masquerading | T1036 |

---

## Analyst Notes

No malicious payloads or attachments were identified during analysis. The email primarily relied on social engineering and embedded hyperlinks to encourage user interaction.

## Skills Demonstrated

- Email Header Analysis
- Threat Identification
- IOC Extraction
- URL and Domain Analysis
- Phishing Detection
- Social Engineering Awareness
- Security Investigation Documentation
- Threat Reporting

Although threat intelligence checks returned clean results, the overall email characteristics remain suspicious due to impersonation attempts and authentication anomalies.
