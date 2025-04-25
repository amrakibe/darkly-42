# 📄 14-Web-Scraping

## 📌 Breach Name: **HiddenDirectoryFlagHunt**

---

## 📖 Description:
This breach exploits hidden directories and obscured file structures on a web server. The challenge involves discovering concealed paths through examination of the robots.txt file, followed by navigating through a complex maze of nested directories to locate a specific README file containing the flag.

The difficulty lies in the extensive directory structure designed to overwhelm manual exploration, requiring the use of automated tools and command-line techniques to efficiently search through all potential locations.

---

## 📌 Vulnerability Type:
- **Information Disclosure**
- **Security Through Obscurity**
- **Insufficient Access Controls**
- **Hidden Resource Exposure**

---

## 📖 Exploitation Process:

1. **Initial Reconnaissance:**
   - Checked the robots.txt file at `http://192.168.224.128/robots.txt`
   - Discovered disallowed directories including `/whatever` and `/.hidden`

2. **Directory Exploration:**
   ```
   User-agent: *
   Disallow: /whatever
   Disallow: /.hidden
   ```

3. **Hidden Directory Discovery:**
   - Accessed `http://192.168.224.128/.hidden`
   - Found an extensive directory structure with multiple nested folders:
   ```
   Index of /.hidden/
   ../
   amcbevgondgcrloowluziypjdh/
   bnqupesbgvhbcwqhcuynjolwkm/
   ceicqljdddshxvnvdqzzjgddht/
   ...
   zzfzjvjsupgzinctxeqtzzdzll/
   README
   ```

4. **Automated Extraction:**
   - Used wget to recursively download all directories and files:
   ```bash
   wget -erobots=off --no-parent --recursive --level=inf http://192.168.224.128/.hidden/
   ```

5. **Systematic Search:**
   - Performed a targeted search for README files containing the flag:
   ```bash
   find . -type f -name "README" -exec grep -H "flag" {} \;
   ```

6. **Flag Discovery:**
   - Located the flag in a deeply nested README file:
   ```
   ./whtccjokayshttvxycsvykxcfm/igeemtxnvexvxezqwntmzjltkt/lmpanswobhwcozdqixbowvbrhw/README:Hey, here is your flag : d5eec3ec36cf80dce44a896f961c1831a05526ec215693c8f2c39543497d4466
   ```

---

## 📌 Security Recommendations:

1. **Proper Access Controls:**
   - Implement authentication for sensitive directories
   - Do not rely on obscurity for security

2. **Web Server Configuration:**
   - Configure the web server to prevent directory listing
   - Use .htaccess or equivalent to restrict access to sensitive paths

3. **Secret Management:**
   - Do not store sensitive information or flags in plaintext files
   - Implement proper encryption or authentication for accessing secure content

4. **robots.txt Best Practices:**
   - Do not disclose sensitive directories in robots.txt
   - Remember that robots.txt is publicly accessible and merely a suggestion for bots

5. **Defensive Design:**
   - Avoid creating unnecessarily complex directory structures
   - Implement logging to detect unusual access patterns or directory traversal attempts

---

## 📌 Impact:
An attacker could discover sensitive information hidden in obscure locations on the web server. While this approach requires patience and the right tools, it demonstrates that hiding information in complex directory structures offers no real security and can be overcome with simple automation techniques.

---

## 📌 Flag:
```
d5eec3ec36cf80dce44a896f961c1831a05526ec215693c8f2c39543497d4466
```