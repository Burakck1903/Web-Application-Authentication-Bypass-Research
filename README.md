# 🛡️ Web Application Security Research: Authentication Bypass (Logic Flaw)

**Target:** Yemeksepeti (Web Platform)  
**Vulnerability Type:** Business Logic Error / Improper Error Handling  
**Date of Discovery:** [Bulduğun Tarih, örn: 2024]  
**Researcher:** Burak Çetinkaya

## 🚨 Executive Summary
This research documents a critical **Business Logic Flaw** found in the user registration flow of a major food delivery platform (Yemeksepeti). The vulnerability allows an attacker to bypass the SMS verification (OTP) step by manipulating the client-side error handling mechanism, resulting in the creation of unverified accounts with arbitrary phone numbers.

## 🔍 Technical Analysis

### The Vulnerability
The application fails to enforce server-side validation for the completion of the SMS verification step. When the system returns an error due to an invalid or unverified phone number, the client-side application does not terminate the registration process. instead, it allows the user to proceed if the error is suppressed or ignored.

**Vulnerability Class:**
* **CWE-20:** Improper Input Validation
* **CWE-799:** Improper Control of Interaction Frequency (Logic)

### 🛠️ Reproduction Steps (Proof of Concept)

1.  **Initiate Registration:** Navigate to the sign-up page and enter user details.
2.  **Input Phone Number:** Enter any arbitrary or already registered phone number.
3.  **Trigger Error:** The system detects the issue and throws a client-side error/warning modal.
4.  **Bypass Logic:** By manipulating the request flow (or simply ignoring the blocking modal via browser tools), the "Submit" action continues to execute.
5.  **Result:** The account is created successfully without a valid SMS OTP code.

## 🎥 Proof of Concept (Video)

The following video demonstrates the exploitation of this vulnerability in a live environment:

[👉 Click Here to Watch the PoC Video](https://youtu.be/Ij0EyxCWW5w)

*(Note: The video is unlisted and provided for educational/research purposes only.)*

## ⚠️ Impact
* **Fraudulent Orders:** Attackers can create mass fake accounts to abuse "New User" coupons and discounts.
* **Data Integrity:** The database becomes polluted with unverified/fake phone numbers.
* **Service Abuse:** Bypassing security controls intended to limit one account per person.

---

### ⚖️ Legal Disclaimer
This repository is for **educational and research purposes only**. The vulnerability was identified during security analysis and is documented here to demonstrate technical competency in Web Application Security. No malicious damage was caused to the service provider.
