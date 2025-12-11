# 🛡️ Web Security Academy Lab: SSRF with Blacklist-Based Input Filter
## 🧠 Objective
Exploit a Server-Side Request Forgery (SSRF) vulnerability that uses a blacklist-based input filter to bypass restrictions and access internal admin functionality.

## 🧩 Step-by-Step Exploitation Walkthrough
### 🔍 Step 1: Reconnaissance

I began by analyzing the product page, which included a “Check stock” feature. This triggered a POST request to /product/stock, with a stockApi parameter pointing to an external service. This hinted at SSRF potential.

<img width="929" height="794" alt="Screenshot 2025-10-12 174029" src="https://github.com/user-attachments/assets/ab795ed9-6eb0-4ee0-a870-e4d5c8e01425" />

<img width="634" height="218" alt="Screenshot 2025-10-12 174103" src="https://github.com/user-attachments/assets/4b058bae-0e99-4f68-998d-d491e3196d06" />

### 🧪 Step 2: Intercepting the Request

Burp Suite's HTTP history is showing a POST to /product/stock Using Burp Suite, I intercepted the request and found the stockApi parameter pointing to:
```
https://stock.weliketoshop.net:443/product/stock/check?productId=1&storeId=1
```

<img width="818" height="397" alt="image" src="https://github.com/user-attachments/assets/c78ccabe-69f8-4262-9b6e-39a9e2df1fd7" />


<img width="488" height="500" alt="image" src="https://github.com/user-attachments/assets/f764a1be-395c-4fb7-90d5-6c3004c80e77" />


This confirmed that the server was making outbound requests based on user input.

### 🧬 Step 3: Testing Localhost Access

Modified request with:

```
stockApi=http://127.0.0.1/admin
```

This was blocked by the blacklist filter, returning:
"External stock check blocked for security reasons"

<img width="493" height="200" alt="Screenshot 2025-10-12 174741" src="https://github.com/user-attachments/assets/50e72fc7-e931-46a7-ac28-c21aa5365c73" />

### 🧪 Step 4: Bypassing the Blacklist

Encoded payloads like:
```
http%3A%2F%2F127.1%2Fadmin
```

<img width="488" height="500" alt="image" src="https://github.com/user-attachments/assets/b8d1a2f5-2e02-467f-9a40-9439e3f17cdb" />


and
```
http://127.1%2F%2561dmin
```

<img width="796" height="425" alt="image" src="https://github.com/user-attachments/assets/2d56eee1-d72a-4a4c-80d5-c33c246cc3c0" />


I used techniques like:

Alternate IP representations (127.1, 2130706433)

Double URL encoding (%2561dmin → %61dmin → admin) These payloads bypassed the blacklist and reached internal endpoints.

<img width="486" height="333" alt="Screenshot 2025-10-12 181458" src="https://github.com/user-attachments/assets/a8f67ae7-64c9-42e5-bd53-c3333cea111d" />

### 🎯 Step 5: Triggering the Admin Action

POST request to:
```
stockApi=http://127.1/admin/delete?username=carlos
```

<img width="785" height="480" alt="image" src="https://github.com/user-attachments/assets/47c5ad87-a6b4-41ed-b962-7add93c9ee17" />


This SSRF payload successfully reached the internal admin panel and triggered the deletion of the user carlos.

### ✅ Step 6: Lab Completion

The lab confirmed successful exploitation and marked the challenge as complete.

<img width="1782" height="787" alt="image" src="https://github.com/user-attachments/assets/5ea21a09-4bcb-4bbb-a0ed-ed0c29a0b1c3" />


### 🧠 Key Takeaways
Blacklists are weak defenses against SSRF; attackers can use encoding tricks and alternate IP formats.

SSRF can be used to access internal services and perform unauthorized actions.

Always validate and sanitize user input, and use allowlists instead of blacklists.

### 📁 Repository Notes
This writeup is part of my ongoing journey in ethical hacking and web application security. You can find more CTF solutions and lab walkthroughs in my GitHub Portfolio.
