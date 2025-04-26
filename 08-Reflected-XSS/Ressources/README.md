## 📌 Breach Name: **Media Parameter Reflected XSS**

---


## 📌 Vulnerability Type:
- **CWE-79: Improper Neutralization of Input During Web Page Generation ('Cross-site Scripting')**
- **CWE-20: Improper Input Validation**
- **CWE-116: Improper Encoding or Escaping of Output**

---

## 📖 Exploitation Process:

1. **Discovery of the Vulnerable Parameter:**
   - Identified a page that accepts a `src` parameter: `http://10.11.100.193/?page=media&src=nsa`
   - This parameter appeared to control what media content is displayed on the page

2. **Source Code Analysis:**
   - Examined the page source code to understand how the `src` parameter is handled
   - Found that user input from the `src` parameter is passed to an `<object>` tag:
     ```html
     <object data="http://10.11.100.193/images/nsa_prism.jpg"></object>
     ```
   - The application constructs this tag dynamically based on user input without proper validation

3. **Data URI Injection:**
   - Leveraged the HTML `<object>` tag's ability to load content from various sources
   - Used a data URI with Base64-encoded content to inject JavaScript:
     ```
     data:text/html;base64,PHNjcmlwdD5hbGVydCgnSGknKTwvc2NyaXB0Pg==
     ```
   - The Base64 string decodes to: `<script>alert('Hi')</script>`

4. **Payload Construction:**
   - Final malicious URL:
     ```
     http://10.11.100.193/?page=media&src=data:text/html;base64,PHNjcmlwdD5hbGVydCgnSGknKTwvc2NyaXB0Pg==
     ```

5. **Exploitation Result:**
   - The JavaScript code was successfully executed in the browser
   - The alert dialog appeared, confirming the XSS vulnerability
   - The application revealed the flag, indicating successful exploitation

---

## 📌 Security Recommendations:

1. **Input Validation:**
   - Implement strict validation for the `src` parameter
   - Whitelist allowed resources and media types
   - Reject requests with suspicious patterns like `data:` URIs

2. **Output Encoding:**
   - Apply context-appropriate encoding for all user-controlled data
   - HTML-encode special characters before inserting them into HTML elements
   - Use Content Security Policy (CSP) headers to restrict script sources

3. **Resource Restriction:**
   - Limit the `src` parameter to predefined paths or resources
   - Validate that requested resources exist in allowed directories
   - Consider implementing a resource mapping system instead of direct path references

4. **Content-Type Verification:**
   - Validate and enforce expected content types for resources
   - Restrict loading of HTML or JavaScript content where not needed
   - Implement proper MIME type checking

5. **Security Headers:**
   - Implement Content-Security-Policy (CSP) headers to limit script execution sources
   - Use X-XSS-Protection headers as an additional layer of defense
   - Apply strict MIME type checking with X-Content-Type-Options: nosniff

