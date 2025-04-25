# 📄 README.md

## 📌 Breach Name: **PathTraversalBreach**

---

## 📖 Description:
This breach exploits a path traversal (also known as directory traversal) vulnerability in the web application. The application uses a `page` parameter to include or display content, but fails to properly validate or sanitize this input.

By manipulating the `page` parameter with directory traversal sequences (`../`), an attacker can access files outside the intended web directory, including sensitive system files like `/etc/passwd`.

---

## 📌 Vulnerability Type:
- **Path Traversal / Directory Traversal**
- **Improper Input Validation**
- **Insecure File Inclusion**

---
## 📖 Technical Details:

The application accepts a `page` parameter in the URL that likely uses PHP's `include()` or similar functionality to load content. The vulnerable endpoint is:

```
http://192.168.43.45/?page=[page-name]
```

When this parameter is manipulated with path traversal sequences, the application follows these sequences and accesses files outside the web root:

```
http://192.168.43.45/?page=../../../../../../../../../../../etc/passwd
```

The multiple `../` sequences navigate up the directory tree from the web root until reaching the system root, then access the `/etc/passwd` file, which contains sensitive system user information and, in this case, reveals a flag.

---

## 🔍 Exploitation Method:

1. Identify a parameter that appears to load content dynamically (in this case, the `page` parameter)
2. Test for path traversal by injecting `../` sequences to navigate up directories
3. Attempt to access common sensitive files like `/etc/passwd`
4. Analyze the response to confirm successful exploitation

Vulnerable URL:
```
http://192.168.43.45/?page=../../../../../../../../../../../etc/passwd
```

---

## 🛡️ Remediation:

1. **Input Validation and Sanitization:**
   - Implement strict server-side validation for the `page` parameter
   - Remove or encode path traversal sequences (`../`) from user input
   - Use a whitelist approach to only allow specific predefined values

2. **Implement Proper Access Controls:**
   - Run the web application with minimal required privileges
   - Set proper file system permissions to prevent access to sensitive files
   - Utilize a chroot jail or container to isolate the application

3. **Secure File Inclusion:**
   - Use absolute paths with a predefined base directory
   - Avoid passing user input directly to file inclusion functions
   - Consider using mapping tables to translate user inputs to file paths

4. **Additional Measures:**
   - Implement Web Application Firewall (WAF) rules to detect path traversal attempts
   - Regular security testing and code reviews focused on file inclusion vulnerabilities
   - Monitor for unusual file access patterns

---

## 📋 Additional Notes:
- This vulnerability could potentially be used to access other sensitive files beyond `/etc/passwd`
- Path traversal vulnerabilities often indicate fundamental flaws in how an application handles file operations
- The presence of a flag in the `/etc/passwd` file suggests this might be part of a deliberately vulnerable application for security training purposes