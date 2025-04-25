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
   - Found the following content:
     ```
     User-agent: *
     Disallow: /whatever
     Disallow: /.hidden
     ```
   - Noted two disallowed directories: `/whatever` and `/.hidden`

2. **Hidden Directory Investigation:**
   - Accessed `http://192.168.224.128/.hidden`
   - Discovered a large directory structure with cryptic folder names:
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
   - Manual browsing revealed that each directory contained more subdirectories and README files
   - Determined that manual exploration would be impractical due to the vast number of nested directories

3. **Automating the Directory Traversal:**
   - Used wget to recursively download the entire directory structure:
     ```bash
     wget -erobots=off --no-parent --recursive --level=inf http://192.168.224.128/.hidden/
     ```
     - `-erobots=off`: Ignore robots.txt restrictions
     - `--no-parent`: Don't ascend to parent directory
     - `--recursive`: Follow and download linked pages
     - `--level=inf`: No limit on recursion depth (follow all nested directories)
   - This command created a local copy of the entire `.hidden` directory structure with all files

4. **Systematic Flag Search:**
   - Once the download was complete, searched all README files for the word "flag":
     ```bash
     find . -type f -name "README" -exec grep -H "flag" {} \;
     ```
     - `find .`: Start search in current directory
     - `-type f`: Look for files only
     - `-name "README"`: Target files named "README"
     - `-exec grep -H "flag" {} \;`: Execute grep on each file, searching for "flag"
     - The `-H` flag ensures the filename is included in the output

5. **Flag Discovery:**
   - The command returned:
     ```
     ./whtccjokayshttvxycsvykxcfm/igeemtxnvexvxezqwntmzjltkt/lmpanswobhwcozdqixbowvbrhw/README:Hey, here is your flag : d5eec3ec36cf80dce44a896f961c1831a05526ec215693c8f2c39543497d4466
     ```
   - This showed the flag was hidden three levels deep in a specific directory path
   - The flag was successfully retrieved: `d5eec3ec36cf80dce44a896f961c1831a05526ec215693c8f2c39543497d4466`

---

## 📌 Security Recommendations:

1. **Proper Access Controls:**
   - Implement authentication for sensitive directories
   - Do not rely on obscurity for security
   - Use proper authorization mechanisms instead of hiding resources

2. **Web Server Configuration:**
   - Configure the web server to prevent directory listing
   - Use .htaccess or equivalent to restrict access to sensitive paths
   - Implement proper 403 Forbidden responses for restricted areas

3. **Secret Management:**
   - Do not store sensitive information or flags in plaintext files
   - Implement proper encryption or authentication for accessing secure content
   - Consider using a proper secret management solution for sensitive data

4. **robots.txt Best Practices:**
   - Do not disclose sensitive directories in robots.txt
   - Remember that robots.txt is publicly accessible and merely a suggestion for bots
   - Critical areas should be protected by authentication, not just listed in robots.txt

5. **Defensive Design:**
   - Avoid creating unnecessarily complex directory structures
   - Implement logging to detect unusual access patterns or directory traversal attempts
   - Consider rate limiting to prevent automated scraping of website content

---

## 📌 Impact:
An attacker could discover sensitive information hidden in obscure locations on the web server. While this approach requires patience and the right tools, it demonstrates that hiding information in complex directory structures offers no real security and can be overcome with simple automation techniques. This vulnerability exposes the fundamental weakness of "security through obscurity" approaches.

---
