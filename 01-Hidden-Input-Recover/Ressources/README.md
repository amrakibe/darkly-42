# 📄 README.md

## 📌 Breach Name: **RecoverFormBreach**

---

## 📖 Description:
This breach exploits an insecure implementation of a password recovery form in the web application. The system uses a hidden input field containing a hardcoded email address but fails to implement proper server-side validation to prevent manipulation of this field.

By modifying the hidden `mail` parameter value using browser developer tools, it's possible to trigger a password recovery for other email addresses, potentially including administrator accounts, leading to the discovery of the flag.

---

## 📌 Vulnerability Type:
- **Insecure Direct Object Reference (IDOR)**
- **Client-Side Validation Bypass**
- **Missing Server-Side Validation**
- **Hidden Field Manipulation**

---

## 📖 Exploitation Process:

1. **Discovery of the Vulnerable Form:**
   - Located a password recovery form on the website
   - Inspected the page source code to review the form implementation

2. **Source Code Analysis:**
   ```html
   <form action="#" method="POST">
      <input type="hidden" name="mail" value="webmaster@borntosec.com" maxlength="15">
      <input type="submit" name="Submit" value="Submit">
   </form>
   ```

3. **Vulnerability Identification:**
   - Noticed the form contains a hidden input field with a hardcoded email address
   - Observed the email is set to "webmaster@borntosec.com" with a maxlength attribute of 15
   - Recognized that hidden fields can be modified despite not being visible in the user interface

4. **Exploitation Technique:**
   - Used browser developer tools (Inspect Element) to modify the hidden input field
   - Changed the email value from "webmaster@borntosec.com" to another email address that might have elevated privileges
   - Alternatively, intercepted the POST request using a proxy tool and modified the "mail" parameter
   - Submitted the form with the modified value

5. **Result:**
   - The application processed the request with the manipulated email address
   - Server-side logic triggered a password recovery for the specified account
   - The response revealed the flag or sensitive information

---

## 📌 Security Recommendations:

1. **Never Trust Client-Side Data:**
   - Assume all client-side data, including hidden fields, can be manipulated
   - Implement proper server-side validation for all input parameters

2. **Implement Proper Authentication:**
   - Require authentication before allowing password recovery for specific accounts
   - Implement additional verification steps (security questions, verification codes)

3. **Use Email Verification:**
   - Send recovery links to the email address being recovered
   - Do not reveal sensitive information directly in the web interface

4. **Input Validation:**
   - Validate email address format and authorized domains
   - Implement rate limiting for password recovery attempts
   - Use allowlists instead of hardcoded values when possible

5. **Secure Coding Practices:**
   - Avoid storing sensitive information in hidden fields
   - Use server-side session variables instead of client-side parameters for critical operations

---

## 📌 Impact:
An attacker could potentially trigger password recovery processes for arbitrary accounts, including administrative ones, potentially leading to account takeover, privilege escalation, or unauthorized access to sensitive information and functionality.