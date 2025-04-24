📌 Name:
# User-Agent & Referer Header Based Access Control Bypass

# 📖 Description:
During source code review, a hidden comment hinted to use a specific User-Agent string:
ft_bornToSec

Another comment suggested a page might require the user to originate from:
https://www.nsa.gov/

Combining both in HTTP request headers provided access to a hidden flag within a specific redirect page.

# 📌 Vulnerability Type:
Insecure Access Control
Security by Obscurity
Referer + User-Agent Based Access

📖 Exploit Method:
🛠️ Command


curl -e "https://www.nsa.gov/" \
     -A "ft_bornToSec" \
     "http://10.11.100.193/index.php?page=b7e44c7a40c5f80139f0a50f3650fb2bd8d00b0d24667c4c2ca32c88e13b758f" \
     | grep flag



This reveals the hidden flag within the response body.



1️⃣  -e "https://www.nsa.gov/"
👉 This sets the Referer header in the HTTP request.

Some web apps try to limit access to certain pages based on where the request “came from”.

In this challenge, the source code hinted:

<!--You must come from : "https://www.nsa.gov/".-->
So, this flag bypasses that weak check by faking the referer.

2️⃣  -A "ft_bornToSec"
👉 This sets the User-Agent header.

In the source code:
<!--Let's use this browser : "ft_bornToSec". It will help you a lot.-->






# 🛡️ Mitigation:
Do not rely on Referer or User-Agent headers for access control. These headers can be easily spoofed by an attacker using tools like curl, Burp Suite, or browser extensions.
Better approaches:

✅ Use proper authentication and authorization mechanisms (e.g., session tokens, API keys, OAuth, etc.)

✅ Avoid exposing hidden routes via source comments — treat client-side code as fully visible.

✅ Implement server-side access controls that check for valid, authenticated, and authorized sessions before serving protected content.

✅ Monitor and log unusual User-Agent strings or Referer headers to detect possible abuse attempts.

✅ Employ security through transparency rather than obscurity — any security relying solely on "hiding things" is inherently weak.

