# 🛡️ Cloudflare WAF Security Project (Basic Security WAF Setup)

**Domain:** https://ivanslab.com  


This project demonstrates how I made and tested a complete **Web Application Firewall (WAF)** protection using Cloudflare.


# **The goal of this project is to demonstrate:**

-My ability to use Cloudflare’s security features, including Security Rules, WAF settings, Security Analytics, and DNS configuration.

-My understanding of common web attacks such as SQL Injection (SQLi), Cross-Site Scripting (XSS), Remote Code Execution (RCE), Directory Traversal, incorrect HTTP methods, and bot patterns like missing cookies. 

-My skills in creating both Cloudflare’s automated ML-based rules and custom regex rules for detection and protection.

-My ability to configure, test, and validate WAF rules using practical cURL-based testing and Cloudflare’s event logs.


# Project Overview

I implemented **12 Cloudflare WAF Rules**:

1. **No-Cookie Challenge**
2. **Wrong HTTP Method Blocking**
3. **SQL Injection Attack Score**
4. **XSS Attack Score**
5. **RCE Attack Score**
6. **WAF Overall Attack Score**
7. **Custom Regex: SQL Injection Detection**
8. **Custom Regex: XSS Detection**
9. **Custom Regex: RCE Detection**
10. **Directory Traversal Blocking**
11. **Missing Headers**



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

## **4. No-Cookie Challenge**
**Purpose:** Detect users that do not support cookies, which is common for bots.\
**Expression:** (http.cookie eq "")\
**Screenshot:**\
<img width="635" height="539" alt="rule" src="https://github.com/user-attachments/assets/8aca07eb-b41a-4407-9161-a4652d02da2a" />

---

## **5. No Headers Rule**
**Purpose:** Catch bots that send requests with missing headers.\
**Expression:**  not any(http.request.headers.names[*] eq "sec-ch-ua")\
**Screenshot:**\
<img width="1297" height="723" alt="rule" src="https://github.com/user-attachments/assets/7d7ad4d2-cc3a-4306-9c8b-9a29c6632f3a" />

---

## **6. Wrong HTTP Method**
**Purpose:** Reduces the attack surface by restricting traffic to standard HTTP methods (GET, POST, HEAD, OPTIONS) and blocks all others (like PUT, DELETE, TRACE).\
**Expression:**  (not http.request.method in {"GET" "POST" "HEAD" "OPTIONS"})\
**Screenshot:**\
<img width="634" height="611" alt="rule" src="https://github.com/user-attachments/assets/2e8e6cd5-c857-433f-8015-8eb99fc5ca99" />

---

## **7. No-Cookie Challenge**
**Purpose:** Detect users that do not support cookies, which is common for bots.\
**Expression:** (http.cookie eq "")\
**Screenshot:**\
<img width="635" height="539" alt="rule" src="https://github.com/user-attachments/assets/8aca07eb-b41a-4407-9161-a4652d02da2a" />

---

## **8. No Headers Rule**
**Purpose:** Catch bots that send requests with missing headers.\
**Expression:**  not any(http.request.headers.names[*] eq "sec-ch-ua")\
**Screenshot:**\
<img width="1297" height="723" alt="rule" src="https://github.com/user-attachments/assets/7d7ad4d2-cc3a-4306-9c8b-9a29c6632f3a" />

---

## **9. Wrong HTTP Method**
**Purpose:** Reduces the attack surface by restricting traffic to standard HTTP methods (GET, POST, HEAD, OPTIONS) and blocks all others (like PUT, DELETE, TRACE).\
**Expression:**  (not http.request.method in {"GET" "POST" "HEAD" "OPTIONS"})\
**Screenshot:**\
<img width="634" height="611" alt="rule" src="https://github.com/user-attachments/assets/2e8e6cd5-c857-433f-8015-8eb99fc5ca99" />

---

## **10. No-Cookie Challenge**
**Purpose:** Detect users that do not support cookies, which is common for bots.\
**Expression:** (http.cookie eq "")\
**Screenshot:**\
<img width="635" height="539" alt="rule" src="https://github.com/user-attachments/assets/8aca07eb-b41a-4407-9161-a4652d02da2a" />

---

## **11. No Headers Rule**
**Purpose:** Catch bots that send requests with missing headers.\
**Expression:**  not any(http.request.headers.names[*] eq "sec-ch-ua")\
**Screenshot:**\
<img width="1297" height="723" alt="rule" src="https://github.com/user-attachments/assets/7d7ad4d2-cc3a-4306-9c8b-9a29c6632f3a" />



Screenshot
<img width="1297" alt="overall-score-rule" src="PLACEHOLDER_LINK_HERE" />
