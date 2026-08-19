# Investigation Report — Brute Force Attack

## Incident Overview

| Field | Details |
|---|---|
| Date of Attack | August 24, 2016 |
| Attack Type | Web Application Brute Force |
| Target System | Joomla CMS — Wayne Corporation |
| Attacker IP | 40.80.148.42 |
| Target URL | /joomla/administrator/index.php |
| Outcome | Successful — Admin panel compromised |

---

## Attack Timeline

| Time | Event |
|---|---|
| 22:03:21 | Attacker begins sending high-volume POST requests to Joomla admin panel |
| 22:03:23 | Requests continue at rapid pace — automated tool confirmed |
| 22:03:25+ | Attacker receives HTTP 200 — successful login achieved |

---

## Evidence Analysis

### 1. High Volume POST Requests
- IP `40.80.148.42` sent **11,923 POST requests** to the Joomla search and admin endpoints
- Normal user behavior = 1-5 requests
- 11,923 requests = automated brute force tool (e.g. Hydra, Burp Suite Intruder)

### 2. Successful Authentication Confirmed
- HTTP Status **200** received **12 times** on admin login page
- This confirms the attacker successfully guessed the admin password
- HTTP Status **303** (redirect) also seen — consistent with post-login redirect behavior

### 3. Secondary Suspicious IP
- IP `23.22.63.114` also accessed `/joomla/administrator/index.php` 
- **412 POST requests** from this IP
- Likely a secondary attacker or the same threat actor using multiple IPs

---

## False Positive Analysis

**Could this be legitimate traffic?**

| Check | Result |
|---|---|
| Is 11,923 requests normal? | No — automated tool confirmed |
| Could it be a web crawler? | No — crawlers use GET, not POST on login pages |
| Could it be a load test? | No — no prior notification, external IP |
| Is HTTP 200 on admin login normal? | Only if correct credentials used |

**Conclusion:** This is a **True Positive** — confirmed brute force attack with successful compromise.

---

## Attacker Profile

| Field | Details |
|---|---|
| Attacker IP | 40.80.148.42 |
| Secondary IP | 23.22.63.114 |
| Tool Used | Likely automated brute force tool |
| Target | Joomla Administrator Panel |
| Motive | Gain admin access to CMS |
