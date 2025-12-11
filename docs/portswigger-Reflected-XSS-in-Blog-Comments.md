# 🛡️ Web Security Academy Lab: Reflected XSS in Blog Comments
## 🧠 Objective
Exploit a reflected Cross-Site Scripting (XSS) vulnerability in a blog comment form to execute arbitrary JavaScript in the victim’s browser.

## 🧩 Step-by-Step Exploitation Walkthrough
**🔍 Step 1: Identifying the Injection Point**

I began by inspecting the blog's comment form. The presence of multiple input fields and a visible post URL suggested that user input might be reflected back into the page.

<img width="794" height="565" alt="Screenshot 2025-10-07 141632" src="https://github.com/user-attachments/assets/229728dd-0c10-4f2f-9e45-76c1c30cc8c0" />

**🧪 Step 2: Crafting the XSS Payload**
I injected a basic JavaScript payload into the comment field. This payload is designed to trigger a browser alert if the input is rendered without proper sanitization.

<img width="763" height="616" alt="image" src="https://github.com/user-attachments/assets/94b753d1-8bf0-45bc-b931-3551230be5c7" />


**🚨 Step 3: Submitting the Malicious Comment**

After submitting the form, the payload was reflected back into the page and executed, confirming the vulnerability.


**✅ Step 4: Payload Execution**
Screenshot Reference: Pop-up dialog with domain and number The alert box appeared, proving that the script was executed in the browser context. This validated the presence of a reflected XSS vulnerability.

<img width="604" height="255" alt="image" src="https://github.com/user-attachments/assets/0ca3d2b7-277a-41a3-88fd-96b7888b1102" />


**🎉 Step 5: Lab Completion**

"Congratulations, you solved the lab!" The lab confirmed successful exploitation of the XSS vulnerability.

### 🧠 Key Takeaways
Reflected XSS occurs when user input is immediately echoed back in the response without proper encoding or sanitization.

Even simple payloads like <script>alert(1)</script> can confirm the presence of XSS.

Always validate and escape user input on both client and server sides.

### 📁 Repository Notes
This writeup is part of my ongoing journey in web application security. You can find more CTF solutions and lab walkthroughs in my GitHub Portfolio.
