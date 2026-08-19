# Incident Report — Web Brute Force Attack

**Report ID:** INC-2016-001  
**Severity:** High  
**Status:** Closed  
**Analyst:** Nitin  

---

## 1. Executive Summary

On August 24, 2016, Wayne Corporation's Joomla CMS was targeted by a brute force attack originating from IP `40.80.148.42`. The attacker sent over 11,900 automated POST requests to the Joomla administrator login page. The attack was successful — the attacker gained access to the admin panel.

---

## 2. Incident Details

| Field | Details |
|---|---|
| Incident ID | INC-2016-001 |
| Date Detected | August 24, 2016 |
| Attack Type | Web Application Brute Force |
| Severity | High |
| Target | Joomla CMS Admin Panel |
| Attacker IP | 40.80.148.42 |
| Secondary IP | 23.22.63.114 |
| Outcome | Successful compromise |

---

## 3. Root Cause

- No account lockout policy was configured on the Joomla admin panel
- No rate limiting or CAPTCHA on the login page
- Weak admin password that could be guessed by automated tool
- No alerting in place for high-volume login attempts

---

## 4. Impact Assessment

| Area | Impact |
|---|---|
| Confidentiality | High — Admin credentials compromised |
| Integrity | High — Attacker could modify website content |
| Availability | Medium — Service could be disrupted |
| Reputation | High — Customer-facing website at risk |

---

## 5. Response Actions Taken

1. Identified attacker IP `40.80.148.42` via HTTP stream logs
2. Confirmed successful login via HTTP 200 status on admin endpoint
3. Flagged secondary IP `23.22.63.114` for further investigation
4. Documented full attack timeline and evidence

---

## 6. Recommended Remediation

| Action | Priority |
|---|---|
| Block attacker IPs at firewall | Immediate |
| Reset all Joomla admin credentials | Immediate |
| Enable account lockout after 5 failed attempts | High |
| Implement CAPTCHA on admin login page | High |
| Enable MFA for admin panel access | High |
| Review Joomla admin logs for post-compromise activity | High |
| Patch Joomla to latest version | Medium |

---

## 7. MITRE ATT&CK Mapping

| Tactic | Technique | ID |
|---|---|---|
| Credential Access | Brute Force | T1110 |
| Credential Access | Password Guessing | T1110.001 |
| Initial Access | Valid Accounts | T1078 |

---

## 8. Conclusion

This was a confirmed **True Positive** brute force attack. The attacker successfully compromised the Joomla admin panel due to absence of basic security controls. Immediate remediation is required to prevent further damage.
