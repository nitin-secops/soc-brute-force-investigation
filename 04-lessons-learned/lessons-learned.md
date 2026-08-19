# Lessons Learned — Brute Force Investigation

**Incident ID:** INC-2016-001  
**Date:** August 24, 2016  
**Analyst:** Nitin  

---

## 1. What Went Wrong

| Issue | Detail |
|---|---|
| No account lockout | Attacker could attempt unlimited passwords |
| No rate limiting | 11,923 requests went unblocked |
| No CAPTCHA | Automated tools worked without any challenge |
| Weak password | Admin password was guessable |
| No alerting | Attack went undetected until log review |

---

## 2. What We Learned

### Detection
- High volume POST requests to login pages are a strong indicator of brute force
- HTTP Status 200 on admin login after repeated failures = confirmed compromise
- Stream HTTP logs are valuable for detecting web-based attacks
- Single IP sending thousands of requests in seconds = automated tool

### Investigation
- Always check response status codes — not just request volume
- Secondary IPs should always be investigated (23.22.63.114 in this case)
- Correlating multiple log sources gives a clearer attack picture

### Response
- Speed matters — account lockout should be automatic, not manual
- Attacker IPs should be blocked at firewall immediately upon detection
- Admin credentials must be rotated after any suspected compromise

---

## 3. Improved Detection Rules

### Rule 1 — Brute Force Alert
**Trigger:** More than 100 POST requests from single IP to login page within 60 seconds  
**Action:** Auto-block IP + alert SOC analyst

### Rule 2 — Successful Login After Multiple Failures
**Trigger:** HTTP 200 on admin login page after 10+ failed attempts  
**Action:** Immediate alert — possible account compromise

### Rule 3 — After-Hours Admin Access
**Trigger:** Admin panel login outside business hours  
**Action:** Alert SOC analyst for verification

---

## 4. Security Recommendations

| Recommendation | Why |
|---|---|
| Implement account lockout (5 attempts) | Stops brute force automatically |
| Add CAPTCHA to login pages | Blocks automated tools |
| Enable MFA on all admin accounts | Even if password is compromised, attacker can't login |
| Deploy Web Application Firewall (WAF) | Blocks malicious traffic before it hits the app |
| Set up SIEM alerting rules | Detect attacks in real time, not after the fact |
| Regular password audits | Identify and replace weak passwords proactively |

---

## 5. Key Takeaways for SOC Analysts

1. **Volume is a signal** — Normal users don't send 11,000 requests
2. **Status codes tell the story** — Always check if the attack succeeded
3. **Automate detection** — Manual log review is too slow for real-time attacks
4. **Document everything** — Evidence chain is critical for incident response
5. **Think like an attacker** — Understand what they want and how they get it
