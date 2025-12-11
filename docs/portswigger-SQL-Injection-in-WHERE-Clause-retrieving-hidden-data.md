# 🛡️ Web Security Academy Labs: SQL Injection Exploitation
## 🧠 Objective
These labs demonstrate how SQL injection vulnerabilities can be exploited to:

Retrieve hidden data from a database.

### 🧩 SQL Injection in WHERE Clause – Retrieving Hidden Data
**🔍 Step 1: Identifying the Injection Point**

I began by analyzing the URL structure and noticed the category parameter was passed directly to the backend. This hinted at a potential injection point.

<img width="931" height="869" alt="image" src="https://github.com/user-attachments/assets/53a0e44d-6321-47f3-ba46-7bbe545fbea4" />

**🧪 Step 2: Testing for SQL Injection**

Injecting a single quote (') caused a server error, confirming that the input was being processed by a SQL query.

<img width="621" height="170" alt="image" src="https://github.com/user-attachments/assets/c09ba6e7-f4be-4ea6-aa18-97437ffcfd66" />


**🧬 Step 3: Crafting the Payload**

I used the classic ' OR 1=1-- payload to bypass the WHERE clause condition. This forced the query to return all rows, including hidden data.

<img width="999" height="190" alt="image" src="https://github.com/user-attachments/assets/653cc65f-01b7-402e-8047-6b3f10fe2b80" />


**✅ Step 4: Successful Exploitation**

The lab confirmed that the injection worked and hidden product categories were revealed. Mission accomplished.

<img width="751" height="429" alt="image" src="https://github.com/user-attachments/assets/a0430850-8038-41e8-b8ab-f54b1d555370" />


### 🧠 Key Takeaways
SQL injection can expose hidden or unauthorized data.

Always validate and sanitize user input.

Even simple payloads can have serious consequences.

### 📁 Repository Notes
This writeup is part of my ongoing journey in ethical hacking and web application security. You can find more walkthroughs and lab solutions in my GitHub Portfolio.
