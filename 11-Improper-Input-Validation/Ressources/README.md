# 📄 README.md

## 📌 Breach Name: **Improper-Input-Validation**

---

## 📖 Description:
This breach exploits an insecure implementation of a survey form in the web application. The system uses a dropdown selection input with predefined values (1-10) but lacks proper server-side validation to ensure the submitted value falls within the expected range.

By modifying the value parameter to a number outside the intended range through browser developer tools, it's possible to trigger unexpected behavior in the application, revealing a hidden flag or sensitive data.

---

## 📌 Vulnerability Type:
- **Client-Side Validation Bypass**
- **Improper Input Validation**
- **Hidden Flag Disclosure**

---

## 📖 Exploitation Process:

1. **Discovery of the Vulnerable Form:**
   - Located a survey form with a dropdown selection limited to values 1-10
   - Noticed the form submits automatically when a value is selected (due to onchange event handler)

2. **Source Code Analysis:**
   ```html
   <select name="valeur" onchange="javascript:this.form.submit();">
       <option value="1">1</option>
       <option value="2">2</option>
       <option value="3">3</option>
       <option value="4">4</option>
       <option value="5">5</option>
       <option value="6">6</option>
       <option value="7">7</option>
       <option value="8">8</option>
       <option value="9">9</option>
       <option value="10">10</option>
   </select>
   ```

3. **Vulnerability Exploitation:**
   - Used browser developer tools (Inspect Element) to modify the HTML
   - Added a new option with a higher value outside the intended range:
     ```html
     <option value="42">42</option>
     ```
   - Alternatively, intercepted the request with a proxy tool and modified the "valeur" parameter
   - Submitted the form with the modified value

4. **Result:**
   - The application processed the unexpected value
   - Server-side logic triggered a hidden condition revealing the flag
   - Flag was displayed in the response

---

## 📌 Security Recommendations:

1. **Implement Server-Side Validation:**
   - Always validate input on the server-side, regardless of client-side controls
   - Ensure the submitted values match an allowed whitelist (1-10 in this case)

2. **Sanitize User Input:**
   - Explicitly validate and sanitize all input parameters before processing
   - Reject any values that don't match expected patterns or ranges

---

## 📌 Impact:
An attacker could potentially access hidden functionality, bypass intended limitations, or access unauthorized data by manipulating form values that aren't properly validated server-side.