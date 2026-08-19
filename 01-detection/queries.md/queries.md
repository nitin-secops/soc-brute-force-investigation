# Detection Queries — Brute Force Investigation

## Query 1 — HTTP Traffic Analysis

**Objective:** Identify suspicious IPs with unusually high request volume against the web server.

**SPL Query:**
```
index=botsv1 earliest=0 sourcetype="stream:http"
| stats count by src_ip, uri_path, http_method
| sort -count
| head 20
```

**Finding:**  
IP `40.80.148.42` sent **11,923 POST requests** to `/joomla/index.php/component/search/` — far above any normal user behavior. This volume strongly indicates an automated brute force or scanning tool.

**Analyst Note:**  
A legitimate user would make a handful of requests. 11,923 requests from a single IP to the same endpoint is a clear indicator of automated attack activity.

---

## Query 2 — Attacker Login Verification

**Objective:** Determine whether the attacker successfully authenticated into the Joomla admin panel.

**SPL Query:**
```
index=botsv1 earliest=0 sourcetype="stream:http"
src_ip="40.80.148.42"
uri_path="/joomla/administrator/index.php"
http_method=POST
| stats count by status
| sort -count
```

**Finding:**  
- Status **200** returned **12 times** — successful login confirmed  
- Status **303** returned **2 times** — redirect after login  

**Analyst Note:**  
HTTP 200 on an admin login page after hundreds of POST attempts confirms the brute force attack was successful. The attacker gained access to the Joomla administrator panel.

---

## Summary of Findings

| Indicator | Value |
|---|---|
| Attacker IP | 40.80.148.42 |
| Target | Joomla Administrator Panel |
| Attack Type | Web Brute Force |
| Total Requests | 11,923 POST requests |
| Outcome | Successful — Admin access gained |
| HTTP Status | 200 OK (login successful) |
