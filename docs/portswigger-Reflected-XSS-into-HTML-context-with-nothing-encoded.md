# 🛡️ Web Security Academy Lab: Reflected XSS into HTML context with nothing encoded
## 🧠 Objective
Demonstrate how reflected XSS vulnerabilities can be exploited to execute arbitrary JavaScript in a victim’s browser.

**🔍 Step 1: Identifying the Injection Point**
I began by analyzing the search functionality. The input was reflected directly into the HTML response, suggesting a potential reflected XSS vulnerability.

<img width="1820" height="882" alt="image" src="https://github.com/user-attachments/assets/8161fedb-df40-4fff-be25-3f9b09287c3e" />


**🧪 Step 2: Crafting the Payload**
I injected a basic script tag into the search field. The payload was embedded in the URL and reflected back into the page without encoding.

<img width="786" height="284" alt="Screenshot 2025-10-09 100958" src="https://github.com/user-attachments/assets/f3a1d102-c080-4ad2-acbe-425c0305b610" />

**🚨 Step 3: Executing the Payload**
Upon submitting the search, the browser executed the script, confirming the vulnerability.

<img width="1835" height="857" alt="image" src="https://github.com/user-attachments/assets/589ba099-d511-46be-85a3-445c2f0c5e42" />


**✅ Step 4: Lab Completion**
The lab validated the successful exploitation of reflected XSS.

### 🧠 Key Takeaways
Reflected XSS occurs when user input is immediately echoed back in the response.

Always sanitize and encode user input before rendering it in the browser.

### 📁 Repository Notes
This writeup is part of my ongoing journey in web application security. You can find more CTF solutions and lab walkthroughs in my GitHub Portfolio.
