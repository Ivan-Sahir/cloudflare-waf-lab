# Cloudflare WAF Configuration Project (Basic Security WAF Setup)

**Domain:** https://ivanslab.com  

## Project Overview
This project demonstrates how I made and tested a multi-layered **Web Application Firewall (WAF)** using Cloudflare. The objective was to secure a web application against common OWASP Top 10 vulnerabilities, bot traffic, and protocol abuse.

### I configured **11 custom security rules** ranging from header validation to machine learning-based attack scoring:

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

---

# **The goal of this project is to demonstrate:**

-My ability to use Cloudflare’s security features, including Security Rules, WAF settings, Security Analytics.\
-My understanding of common web attacks such as SQL Injection (SQLi), Cross-Site Scripting (XSS), Remote Code Execution (RCE), Directory Traversal, incorrect HTTP methods, and bot patterns like missing cookies.\
-My skills in creating both Cloudflare’s automated ML-based rules and custom regex rules for detection and protection.\
-My ability to configure, test, and validate WAF rules using practical cURL-based testing and Cloudflare’s event logs.\

---

## Threat Mitigation Architecture

The WAF configuration was designed to provide protection against common **OWASP Top 10 vulnerabilities**, **automated bot traffic**, and **protocol abuse**.

### 1. Mitigating OWASP some of the Top 10 Vulnerabilities
* **Injection (A03):** Made a "Defense in Depth" security using static Regex signatures for obvious attack patterns and Cloudflare AI Scoring to catch advanced SQLi, XSS, and RCE attacks.
* **Broken Access Control (A01):** Used strict URI path validation to block Directory Traversal attempts, preventing unauthorized access to system files.
* **Security Misconfiguration (A05):** Reduced the attack surface by disabling unnecessary HTTP methods (e.g., `PUT`, `DELETE`), ensuring the server only accepts standard traffic.

### 2. Protocol Abuse Prevention
* **Method Enforcement:** Locked the server to only allow standard HTTP traffic (`GET`, `POST`, `HEAD`, `OPTIONS`), preventing attackers from using valid but dangerous methods to interact with the backend.
* **Client Integrity:** Enforced browser header validation (`sec-ch-ua`) to reject headless clients that do not have legitimate browser fingerprints.

### 3. Bot Traffic Management
* **Stateless Bot Challenge:** Configured a "No-Cookie Rule" with JS Chnallenge to automatically challenge clients that do not support cookies or maintain session state, filtering out basic scrapers and scanners.

---
# Project Documentation

### 1. [WAF Rules Implementation](Rules.md)
* Breakdown of all 11 security rules.


### 2. [Testing & Verification]9Tests.md)
* **Evidence:** Logs from `Security -> Analytics -> Events` showing the WAF successfully blocking live attacks.
* **Tests:** Includes tests for no cookie rule, wrong http method, directory traversal, no headers rule, regexe and ML score rule.

---

## Key Results
* Successfully blocked **100%** of simulated attacks.
* Implemented "Defense in Depth" (Static Checks → Signatures → AI Scoring).
* Configured protection for both bots (No-Cookie/No-Headers) and advanced threats (SQLi/RCE/XSS).
