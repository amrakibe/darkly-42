# 📄 14-Web-Scraping

## 📌 Breach Name: **MinimalInputStoredXSS**

---

## 📖 Description:
This breach exploits a stored Cross-Site Scripting (XSS) vulnerability in a message form that unexpectedly processes single-character input in an insecure manner. While complex XSS payloads were filtered out by the application's security mechanisms, a single letter "a" input triggered an anomalous condition that revealed the flag.

This demonstrates a unique edge case in input validation where developers may have focused on filtering known malicious patterns but overlooked basic input handling, resulting in unexpected application behavior with minimal input.

---

## 📌 Vulnerability Type:
- **Stored Cross-Site Scripting (XSS)**
- **Edge Case Input Handling**
- **Input Validation Bypass**
- **Unexpected Application Logic**

---

## 📖 Exploitation Process:

1. **Initial Reconnaissance:**
   - Located a message form on the target application
   - Identified it as a potential injection point for stored XSS

2. **Standard XSS Testing:**
   - Attempted common XSS payloads such as `<script>alert('XSS')</script>`
   - All complex payloads were filtered or blocked by the application
   - The comment containing `alert('XSS')` was specifically removed

3. **Payload Variation:**
   - Tried various XSS vectors using different event handlers and encoding techniques
   - Tested HTML tags like `<img>`, `<svg>`, and `<body>` with event handlers
   - Attempted JavaScript protocol in links and different quote styles
   - All sophisticated attempts continued to be blocked or filtered

4. **Boundary Testing:**
   - After exhausting complex payloads, switched to testing edge cases
   - Tried minimum valid inputs to test boundary conditions
   - Submitted a single character "a" in the form field

5. **Unexpected Result:**
   - The application processed the single letter "a" differently than more complex inputs
   - This triggered an anomalous condition in the application logic
   - The flag was automatically displayed in response to this minimal input

6. **Vulnerability Confirmation:**
   - Repeated the test to confirm consistent behavior
   - The flag was consistently revealed when submitting only the letter "a"
   - This confirmed the presence of unusual application logic specific to minimal input handling

---

## 📌 Security Recommendations:

1. **Comprehensive Input Validation:**
   - Validate all inputs regardless of complexity or length
   - Apply consistent validation rules to all input values
   - Don't focus only on "known bad" patterns; implement proper validation for all inputs

2. **Edge Case Testing:**
   - Include boundary testing in security assessments
   - Test minimum and maximum input lengths
   - Test single characters, empty strings, and other edge cases

3. **Avoid Special Case Logic:**
   - Don't implement special handling for specific input values
   - Ensure application logic treats all inputs consistently
   - Remove any "backdoors" or debug features that activate with specific inputs

4. **Code Review Practices:**
   - Review application logic for unusual conditionals based on specific input values
   - Look for hidden features triggered by specific input patterns
   - Ensure all input handling follows the same security standards

5. **Security Testing Strategy:**
   - Include both complex attack vectors and simple edge cases in testing
   - Don't assume only complex payloads can trigger vulnerabilities
   - Test all input fields with the same rigor regardless of expected content

---
