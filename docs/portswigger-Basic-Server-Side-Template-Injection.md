# 🛡️ Web Security Academy Lab: Basic Server-Side Template Injection
## 🧠 Objective
Exploit a server-side template injection vulnerability to execute arbitrary code on the server and retrieve sensitive information.

## 🧩 Step-by-Step Exploitation Walkthrough
**🔍 Step 1: Reconnaissance**
I began by analyzing the application’s behavior when submitting messages. I checked how the application reacted when clicking the view details button of a produuct that was out of stock. The text parameter appeared to be rendered directly into the HTML response, suggesting a potential injection point.

<img width="921" height="864" alt="Screenshot 2025-10-12 163356" src="https://github.com/user-attachments/assets/f804366c-f4da-4853-976c-977e1d8d9619" />

<img width="921" height="769" alt="Screenshot 2025-10-12 163456" src="https://github.com/user-attachments/assets/2307d1f9-e2df-40eb-88af-4e67e7cd6e87" />

<img width="833" height="765" alt="image" src="https://github.com/user-attachments/assets/93ddfad8-0723-4b5f-b721-7a74158d4653" />


**🧪 Step 2: Testing for Template Injection**
I crafted a payload using JSP-style syntax to test for server-side code execution. The goal was to determine if the server was vulnerable to SSTI.

<img width="833" height="724" alt="image" src="https://github.com/user-attachments/assets/3696d437-5ae0-4f47-98e6-e7be8e3ace4c" />


<img width="380" height="65" alt="image" src="https://github.com/user-attachments/assets/287a2b22-0753-4d2a-ade9-42c1a72ef908" />


**🚨 Step 3: Executing the Payload**
The server executed the injected command and returned the result (carlos), confirming that the template engine was evaluating user input as code.

<img width="835" height="721" alt="image" src="https://github.com/user-attachments/assets/c3074972-a56a-471d-adae-c6a3efe54558" />


**🧬 Step 4: Exploring the File System**
I discovered a file named morale.txt in the server’s directory. This indicated that I could potentially read or manipulate server-side files.

<img width="834" height="727" alt="image" src="https://github.com/user-attachments/assets/8ef20e3c-04cc-43d2-a88c-b4f7d829c5aa" />


<img width="833" height="724" alt="Screenshot 2025-10-12 165624" src="https://github.com/user-attachments/assets/88d3046b-4e35-43e7-9b4c-716ba964d08c" />

<img width="413" height="170" alt="Screenshot 2025-10-12 165639" src="https://github.com/user-attachments/assets/0e78d298-d0a4-4d25-9dea-b6468a8bdbce" />

**🎯 Step 5: Attempting File Deletion**
I sent a payload to delete the morale.txt file using a Unix command. The server accepted and executed the command, demonstrating the severity of the vulnerability.

<img width="462" height="72" alt="Screenshot 2025-10-12 165712" src="https://github.com/user-attachments/assets/ca8d2a2e-b052-4665-8746-1a700e2c9db0" />

<img width="495" height="497" alt="Screenshot 2025-10-12 165948" src="https://github.com/user-attachments/assets/db3ddc7c-9008-4532-a0ed-5c7f02e43976" />

**✅ Step 6: Lab Completion**
After confirming code execution and file manipulation, the lab marked the challenge as complete.

<img width="922" height="202" alt="Screenshot 2025-10-12 170016" src="https://github.com/user-attachments/assets/c9011a9e-4a38-491e-84ed-576d97ecfa40" />

### 🧠 Key Takeaways
SSTI vulnerabilities allow attackers to execute arbitrary code on the server.

Input passed to template engines must be strictly sanitized and validated.

Even basic injection points can lead to full server compromise if exploited properly.

### 📁 Repository Notes
This writeup is part of my ongoing journey in ethical hacking and web application security. You can find more CTF solutions and lab walkthroughs in my GitHub Portfolio.
