# 🛡️ Web Security Academy Lab: Web Shell Upload via Extension Blacklist Bypass
🧠 Objective
The goal of this lab was to bypass a server-side blacklist that restricts certain file extensions (e.g., .php) and successfully upload a web shell to extract sensitive information.

## 🧩 Step-by-Step Exploitation Walkthrough

**🔍 Step 1: Initial Upload Attempt Fails**

I began by attempting to upload a basic PHP web shell (exploit.php) via the avatar upload functionality. The server responded with an error message indicating that .php files were blocked. This confirmed the presence of an extension-based blacklist.

<img width="857" height="603" alt="image" src="https://github.com/user-attachments/assets/79a56d03-baf6-4771-a3c3-43cbccbb44dc" />

<img width="505" height="120" alt="Screenshot 2025-10-06 132341" src="https://github.com/user-attachments/assets/45d39cb1-37c0-4af0-bc0f-4fbd71a4a6bb" />

<img width="847" height="663" alt="image" src="https://github.com/user-attachments/assets/c3d9575b-01b5-43f9-84cd-f7d998061552" />


**🧪 Step 2: Inspecting the Upload Mechanism**

Using Burp Suite, I intercepted the avatar upload request. The multipart/form-data payload revealed the structure of the file upload, including the filename and content-type headers. This gave me insight into how the server processes uploads.

<img width="855" height="624" alt="image" src="https://github.com/user-attachments/assets/b483717b-7906-4aba-80d7-eb9988a604fd" />


<img width="526" height="282" alt="Screenshot 2025-10-07 124610" src="https://github.com/user-attachments/assets/8414060d-c28e-4962-a1c3-54e41f92b0f1" />

**🧬 Step 3: Attempting a Bypass with .php.jpg**

I modified the filename to shrek.php.jpg, hoping the server would treat it as a harmless image while still executing the embedded PHP code. However, the server did not execute the payload, indicating that it likely validated the file content or used a stricter blacklist.

<img width="349" height="167" alt="Screenshot 2025-10-13 194513" src="https://github.com/user-attachments/assets/e281e9f2-f89e-4a09-b8db-01655834e05b" />

<img width="340" height="107" alt="Screenshot 2025-10-13 194534" src="https://github.com/user-attachments/assets/f077d6f5-629b-4ddf-a59b-03223b32cd8f" />

<img width="301" height="199" alt="Screenshot 2025-10-13 194015" src="https://github.com/user-attachments/assets/72125acb-13e4-4bdc-9e01-3ee77145d057" />

<img width="323" height="301" alt="Screenshot 2025-10-13 194040" src="https://github.com/user-attachments/assets/696cf90a-a870-4456-afc3-a65ae8a78413" />

<img width="938" height="679" alt="image" src="https://github.com/user-attachments/assets/e8e17100-42c0-4370-adca-3fb74d270c2d" />


**🧱 Step 4: Uploading .htaccess to Override MIME Handling**

To force the server to treat .jpg files as PHP, I uploaded a .htaccess file with the following content:

apache
AddType application/x-httpd-php .exploit
This instructs the server to interpret .exploit files in the directory as PHP scripts

<img width="863" height="654" alt="image" src="https://github.com/user-attachments/assets/62fef3c6-8dc2-412a-8048-05b78fa1672d" />

<img width="859" height="641" alt="Screenshot 2025-10-07 125924" src="https://github.com/user-attachments/assets/739cf87f-5c9b-4f7a-bb90-ce7109553ed5" />

**🧠 Step 5: Uploading the Web Shell as shrek.exploit**

With the .htaccess file in place, I re-uploaded the web shell disguised as shrek.exploit. The payload contained:

php
<?php echo file_get_contents('/home/carlos/secret'); ?>
This PHP code attempts to read the contents of a sensitive file on the server.

<img width="859" height="638" alt="image" src="https://github.com/user-attachments/assets/65d210ae-1d4f-437b-b02b-13cc63a3c8b2" />

<img width="858" height="667" alt="image" src="https://github.com/user-attachments/assets/763a8d67-b875-40f8-8366-187a712e93d9" />

<img width="695" height="476" alt="Screenshot 2025-10-07 124513" src="https://github.com/user-attachments/assets/9e210e96-cf05-45fd-9433-70e92f2ebc77" />

**✅ Step 6: Successful Execution and Flag Retrieval**

After navigating to the uploaded file by right-clicking on the broken avatar image and opening it in a new tab, the server executed the PHP code and returned the contents of /home/carlos/secret, revealing the flag:

<img width="718" height="466" alt="Screenshot 2025-10-07 130337" src="https://github.com/user-attachments/assets/3dff8016-2608-42ee-a16a-7b503f79eae2" />


<img width="500" height="234" alt="image" src="https://github.com/user-attachments/assets/8d6b94e6-3a28-4e57-a7a8-6636aadaa225" />


**🏁 Step 7: Submitting the Flag**

I submitted the retrieved flag through the lab interface, confirming successful exploitation.

<img width="701" height="349" alt="image" src="https://github.com/user-attachments/assets/e67f9a45-e206-49ad-b768-5839fc76434f" />


**🎉 Step 8: Lab Completion**

The lab acknowledged the successful bypass and payload execution, marking the challenge as complete.

<img width="951" height="381" alt="image" src="https://github.com/user-attachments/assets/9d3aef6e-40c6-49dd-b941-e58b254aebb6" />


### 🧠 Key Takeaways
File extension blacklists can be bypassed using .htaccess overrides.

MIME type and content validation are critical for secure file upload handling.

Burp Suite is an essential tool for intercepting, modifying, and replaying HTTP requests during web application testing.

### 📁 Repository Notes
This writeup is part of my ongoing journey in web application security. You can find more CTF solutions and lab walkthroughs in my GitHub Portfolio.
