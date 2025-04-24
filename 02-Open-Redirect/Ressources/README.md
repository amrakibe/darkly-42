## 🏴‍☠️ Flag Discovery Using Open Redirect Vulnerability
🚀 Overview
This README outlines the steps taken to exploit an open redirect vulnerability in a web application hosted at http://H.H.H.H and find a flag hidden within the system.

## 🔍 Steps to Find the Open Redirect Vulnerability
1. Identify the Vulnerable URL Parameter
The application had a suspicious page parameter that could control redirection behavior. The initial test URL looked like:


http://H.H.H.H/index.php?page=redirect&site=http://malicious.com
This suggested that the site parameter might be a redirect target, hinting at an open redirect vulnerability.

2. Test the Open Redirect
The next step was to manipulate the site parameter to an external URL, testing whether the application properly handled redirection. For example:


http://H.H.H.H/index.php?page=redirect&site=http://malicious.com
The page was redirecting successfully to the http://malicious.com site, confirming the open redirect vulnerability.

3. Search for the Flag Using Open Redirect
After confirming the open redirect, the next step was to redirect the site parameter to a page within the application where the flag might be hidden.

By using the redirection, you were able to access a page that contained the hidden flag:


http://H.H.H.H/index.php?page=redirect&site=http://H.H.H.H/flag_page
This page returned the flag.

4. Using curl to Automate the Flag Retrieval
You can automate the process of fetching the flag using the curl command, with the appropriate headers and URL manipulation:


curl "http://H.H.H.H/index.php?page=redirect&site=http://H.H.H.H/flag_page"
This command successfully retrieved the flag from the vulnerable redirect.

💡 Key Takeaways
Open Redirect: An open redirect vulnerability allows an attacker to manipulate a URL parameter, redirecting users to arbitrary URLs, potentially exposing sensitive pages like flags.

Exploitation: The core of the exploit involved altering the site parameter to redirect to a page that revealed the flag.

Automation: Using curl helped automate the redirection and fetching process, making it faster to retrieve the flag.

🚨 Important Security Notes
Open Redirect Risks: Open redirect vulnerabilities can be abused for phishing attacks, making it crucial to validate and sanitize URL parameters to prevent unauthorized redirects.

Prevention: Always validate and whitelist URL inputs to ensure users cannot redirect to arbitrary or untrusted sites.

