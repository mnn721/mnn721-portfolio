# Firewall Blocked Malicious URL Investigation (True Positive)

## Overview

This investigation documents the analysis of a high-severity firewall alert generated after a workstation attempted to access a known malicious external website. The investigation involved reviewing firewall logs, correlating SIEM events, validating the destination using threat intelligence, and determining the appropriate incident classification.

---

## Alert Information

| Field | Value |
|-------|-------|
| **Alert ID** | 8816 |
| **Severity** | High |
| **Alert Type** | Firewall |
| **Action** | Blocked |
| **Timestamp** | June 28, 2026 - 21:44 UTC |

---

## Objective

Determine whether the outbound connection represented legitimate malicious activity and verify whether the organization's security controls successfully prevented communication with the malicious destination.

---

## Network Details

| Field | Value |
|-------|-------|
| **Source IP** | 10.20.2.17 |
| **Source Port** | 34257 |
| **Destination IP** | 67.199.248.11 |
| **Destination Port** | 80 |
| **URL** | http://bit.ly/3sHkX3da12340 |
| **Application** | Web Browsing |
| **Protocol** | TCP |
| **Firewall Rule** | Blocked Websites |
| **Firewall Action** | Blocked |

---

## Indicators of Compromise (IOCs)

- Source Host: **10.20.2.17**
- Destination IP: **67.199.248.11**
- URL: **http://bit.ly/3sHkX3da12340**
- Firewall Rule: **Blocked Websites**
- Protocol: **TCP**
- Destination Port: **80**

---

## Investigation Process

1. Reviewed the high-severity firewall alert.
2. Identified the source and destination IP addresses.
3. Analyzed SIEM logs to establish a timeline of user activity.
4. Confirmed the user previously performed normal web browsing before attempting to access the blocked URL.
5. Validated the destination IP using TryDetectThis.
6. Confirmed the destination IP was classified as **Malicious**.
7. Verified the firewall successfully blocked the outbound connection before communication could be established.

---

## Timeline

| Time | Event |
|------|-------|
| **21:42** | User performed a legitimate Google search. |
| **21:44** | User attempted to access a shortened URL (bit.ly). |
| **21:44** | Firewall detected the destination as blacklisted and blocked the connection. |
| **21:45** | Threat intelligence confirmed destination IP **67.199.248.11** was malicious. |

---

## Findings

The investigation determined that host **10.20.2.17** attempted to connect to a blacklisted external URL.

Threat intelligence analysis confirmed that destination IP **67.199.248.11** was **Malicious**.

Firewall logs verified that the organization's **Blocked Websites** policy successfully prevented the outbound connection before communication with the malicious destination could be established.

No evidence indicated that the firewall block was bypassed or that the malicious connection was successfully completed.

---

## Incident Classification

**True Positive**

The firewall correctly detected an attempted connection to a confirmed malicious destination and successfully prevented the communication.

---

## Recommendations

- Continue monitoring host **10.20.2.17** for additional suspicious activity.
- Investigate how the user obtained the shortened URL.
- Provide user awareness training regarding phishing attempts and shortened URLs.
- Continue maintaining and updating firewall blocklists and threat intelligence feeds.
- Review firewall logs for additional attempts to communicate with the same malicious destination.

---

## Skills Demonstrated

- Firewall Log Analysis
- SIEM Investigation
- Threat Intelligence Validation
- IOC Identification
- Network Traffic Analysis
- Timeline Analysis
- Incident Classification
- Security Documentation

---

## Tools Used

- TryHackMe SOC Simulator
- Splunk SIEM
- TryDetectThis
- Firewall Logs

---

## Key Takeaways

- Firewall alerts should be validated with threat intelligence before determining incident severity.
- Building a timeline helps establish the sequence of user activity leading to the alert.
- Successfully blocked connections can still represent true positive detections when the destination is confirmed malicious.
- Layered security controls, including firewalls and threat intelligence, play a critical role in preventing successful attacks.

---

## Screenshots

The `screenshots` folder contains evidence collected during the investigation, including:

- Firewall Alert
- Splunk SIEM Investigation
- Timeline Analysis
- Threat Intelligence Results
- Final Case Report
