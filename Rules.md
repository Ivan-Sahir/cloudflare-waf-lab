# All Rules 

## **1. No-Cookie Challenge**
**Purpose:** Detect users that do not support cookies, which is common for bots.\
**Expression:** (http.cookie eq "")\
**Screenshot:**\
<img width="635" height="539" alt="rule" src="https://github.com/user-attachments/assets/8aca07eb-b41a-4407-9161-a4652d02da2a" />

---

## **2. No Headers Rule**
**Purpose:** Catch bots that send requests with missing headers.\
**Expression:**  not any(http.request.headers.names[*] eq "sec-ch-ua")\
**Screenshot:**\
<img width="1297" height="723" alt="rule" src="https://github.com/user-attachments/assets/7d7ad4d2-cc3a-4306-9c8b-9a29c6632f3a" />

---

## **3. Wrong HTTP Method**
**Purpose:** Reduces the attack surface by restricting traffic to standard HTTP methods (GET, POST, HEAD, OPTIONS) and blocks all others (like PUT, DELETE, TRACE).\
**Expression:**  (not http.request.method in {"GET" "POST" "HEAD" "OPTIONS"})\
**Screenshot:**\
<img width="634" height="611" alt="rule" src="https://github.com/user-attachments/assets/2e8e6cd5-c857-433f-8015-8eb99fc5ca99" />

---

## **4. Directory Traversal Blocking**
**Purpose:** Prevent attackers from navigating outside the intended web directory to access sensitive system files by inspecting the request URI for traversal patterns.\
**Expression:**\
(http.request.uri contains "../") or\
(http.request.uri contains "..%2F") or\
(http.request.uri contains "%2e%2e%2f") or\
(http.request.uri contains "..\\") or\
(http.request.uri contains "..%5C") or\
(http.request.uri contains "%2e%2e%5c") or\
**Screenshot:**\
<img width="1401" height="648" alt="rule" src="https://github.com/user-attachments/assets/8c5ee5a4-3a53-49ef-8b60-ce2f57ae14eb" />


---

## **5. Regex: SQL Injection Detection**
**Purpose:** Serve as a backup to the AI scoring system by instantly dropping requests that contain pattern "UNION SELECT" in the URI.
**Expression:** (http.request.full_uri matches "(?i)(union.*select)")\
**Screenshot:**\
<img width="636" height="585" alt="rule" src="https://github.com/user-attachments/assets/fbe35438-1155-4c2e-9ad2-4c00c954bdbe" />


---

## **6. Regex: XSS Detection**
**Purpose:** Block attempts to inject executable JavaScript code into URL parameters by scanning query strings for script tags and protocol handlers.\
**Expression:**\
(http.request.uri.query contains "<script") or\
(http.request.uri.query contains "%3Cscript") or\
(http.request.uri.query matches "(?i)javascript:") or\
(http.request.uri.query matches "(?i)<img") or\
(http.request.uri.query matches "(?i)<svg") or\
(http.request.uri.query matches "(?i)onerror=")\
**Screenshot:**\
<img width="1443" height="628" alt="rule" src="https://github.com/user-attachments/assets/9ba52d3f-2dd6-4bab-bc45-967df8beeeb1" />

---

## **7. Regex: RCE Detection**
**Purpose:** Detect and stop attempts to do malicious payloads or interact with the server shell by targeting command injection syntax and common tools (e.g. curl).\
**Expression:** (http.request.full_uri matches r"(?i)(;|&&|\|\||\$\(|wget|curl|/bin/sh|/etc/passwd)")\
**Screenshot:**\
<img width="617" height="614" alt="rule" src="https://github.com/user-attachments/assets/00042f90-fd55-497e-8a94-fd59ce12c25f" />

---

## **8. SQL Injection Attack Score**
**Purpose:** Cloudflare’s machine learning WAF to dynamically block requests with an SQL Injection (SQLi) score of 30 or lower, protecting the database without relying solely on static signatures.\
**Expression:** (cf.waf.score.sqli le 30)\
**Screenshot:**\
<img width="636" height="596" alt="rule" src="https://github.com/user-attachments/assets/542f883d-563c-4f7c-b25c-518b7a1575e7" />

---

## **9. XSS Attack Score**
**Purpose:** Protects from malicious scripts by blocking requests flagged by Cloudflare’s AI detection system as likely Cross-Site Scripting (XSS) attacks with score of 30 or lower.\
**Expression:**  (cf.waf.score.xss le 30)\
**Screenshot:**\
<img width="650" height="614" alt="rule" src="https://github.com/user-attachments/assets/a199cac4-2730-4107-9757-ccac96810255" />

---

## **10. RCE Attack Score**
**Purpose:** Prevent the execution of commands on the server by blocking requests identified by the Cloudflare’s AI scoring system as potential Remote Code Execution (RCE) attempts with score of 30 or lower.\
**Expression:** (cf.waf.score.rce le 30)\
**Screenshot:**\
<img width="636" height="594" alt="rule" src="https://github.com/user-attachments/assets/2e4bb5f2-ac1d-43cb-89fd-5c47dc6a25a2" />

---

## **11. WAF Overall Attack Score**
**Purpose:** Comprehensive security net blocking any request with oveall attack probabiity score of 30 or lower, using data from multiple attack vectors to catch different threats.\
**Expression:**  (cf.waf.score le 30)\
**Screenshot:**\
<img width="635" height="597" alt="rule" src="https://github.com/user-attachments/assets/e6797645-a78e-4a50-98dd-874019551cda" />
