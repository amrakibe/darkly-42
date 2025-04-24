# 📄 README.md

## 📌 Breach Name: **RobotsAdminBreach**

---

## 📖 Description:
This breach exploits information disclosure through the robots.txt file and weak credential storage practices. By examining the disallowed directories in robots.txt, an attacker can discover hidden resources containing administrator credentials, which can then be used to access the restricted admin area and retrieve the flag.

---

## 📌 Vulnerability Type:
- **Information Disclosure**
- **Insecure Credential Storage**
- **Weak Authentication Mechanism**
- **Improper Access Control**

---

## 📖 Exploitation Process:

1. **Discovery through robots.txt:**
   - Accessed the robots.txt file at `http://10.11.100.193/robots.txt`
   - Found two disallowed directories:
     ```
     User-agent: *
     Disallow: /whatever
     Disallow: /.hidden
     ```

2. **Exploration of Disallowed Directories:**
   - Navigated to the `/whatever` directory
   - Found directory listing enabled, revealing the contents:
     ```
     Index of /whatever/
     ../
     htpasswd                                           29-Jun-2021 18:09                  38
     ```

3. **Credential Discovery:**
   - Accessed the htpasswd file
   - Found administrator credentials stored in an insecure format:
     ```
     root:437394baff5aa33daa618be47b75cb49
     ```
   - Identified that the password was hashed using MD5 encryption

4. **Password Cracking:**
   - Recognized the hash as MD5 format
   - Successfully cracked the MD5 hash to reveal the plaintext password: `qwerty123@`

5. **Administrator Access:**
   - Located the admin login page at `/admin`
   - Successfully authenticated using the discovered credentials:
     - Username: `root`
     - Password: `qwerty123@`
   - After login, gained access to restricted content containing the flag

---

## 📌 Security Recommendations:

1. **Secure robots.txt Configuration:**
   - Don't list sensitive directories in robots.txt as it serves as a roadmap for attackers
   - Avoid disclosing the existence of admin interfaces or security-related paths

2. **Secure Credential Storage:**
   - Never store passwords using weak hashing algorithms like MD5
   - Implement proper password hashing using modern algorithms (bcrypt, Argon2, etc.) with appropriate salting
   - Use strong, complex passwords that resist common cracking techniques

3. **Directory Listing:**
   - Disable directory listing on all web servers to prevent information disclosure
   - Implement proper .htaccess or equivalent configurations

4. **Access Control:**
   - Implement proper authentication mechanisms with multi-factor authentication for admin areas
   - Use IP restrictions or other additional security layers for sensitive administrative functions
   - Implement proper session management with secure cookies and timeouts

5. **Regular Security Audits:**
   - Regularly scan for misconfigured services and unauthorized access points
   - Monitor access logs for unusual patterns or brute force attempts

---

## 📌 Impact:
An attacker could gain unauthorized access to the administrator interface, potentially leading to complete system compromise, data theft, or service disruption. In this case, the vulnerability allowed direct access to sensitive information (the flag) that should have been protected.