# Cloudflare WAF Security Project (Basic Security WAF Setup)

**Domain:** https://ivanslab.com  


This project demonstrates how I made and tested a **Web Application Firewall (WAF)** protection using Cloudflare.


# **The goal of this project is to demonstrate:**

-My ability to use Cloudflare’s security features, including Security Rules, WAF settings, Security Analytics, and DNS configuration.\
-My understanding of common web attacks such as SQL Injection (SQLi), Cross-Site Scripting (XSS), Remote Code Execution (RCE), Directory Traversal, incorrect HTTP methods, and bot patterns like missing cookies.\
-My skills in creating both Cloudflare’s automated ML-based rules and custom regex rules for detection and protection.\
-My ability to configure, test, and validate WAF rules using practical cURL-based testing and Cloudflare’s event logs.\


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
