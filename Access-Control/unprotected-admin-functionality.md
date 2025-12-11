# **PortSwigger – Unprotected Admin Functionality (IDOR / BAC)**

---

## 🔹 **Lab Information**

**Lab Name:** Unprotected admin functionality  
**Level:** 1  
**Vulnerability Type:**

- Broken Access Control
- Unprotected Admin Panel
- Functional IDOR
    

---

## 🔹 **Vulnerability Description**

The problem in this lab is that the admin panel can be accessed **without logging in** and without any authorization checks.  

This means anyone—even without an account—can open the admin page and perform dangerous actions like deleting users.

This is a serious issue because an attacker can control the system easily just by knowing the admin URL

---

## 🔹 **Step-by-Step Exploitation**

#### 1) **Checking robots.txt**

I opened `/robots.txt` and found:

`Disallow: /administrator-panel`

This revealed the admin panel path.

---
### **2) Accessing the Admin Panel**

I opened the link:

`/administrator-panel`

The admin page loaded without login, which confirms a Broken Access Control issue.

---

### **3) Deleting the user “carlos”**

Inside the admin panel, I found a delete option.  
I selected the user:

`carlos`

Then clicked **Delete**, and the account was removed


---


## 🔹 **Impact**

This vulnerability is **Critical** because an attacker can:

- Access the admin panel without permissions
- Delete or edit users
- View sensitive data
- Take full control of the application
    

In real scenarios, this could lead to full compromise and data leaks
    

---

## 🔹 **Root Cause**

- No authorization checks in place
    
- Relying on hiding the admin path
    
- Admin interface not properly integrated with authentication/session system
    

---

## 🔹 **Fix Recommendations**

✔ **Implement authorization checks**  
The server must verify:

- User session
    
- User role
    
- Authorization tokens
    

✔ **Do NOT rely on robots.txt for security**  
It should not contain sensitive paths.

✔ **Protect admin interfaces on the server side**  
Changing the URL alone is not enough.

✔ **Enable logging and monitoring**  
To detect unauthorized access attempts.

---

## 🔹 **Evidence**

- `robots.txt` reveals the admin panel
    
- Direct access to the admin page without login
    
- Deleting user “carlos” from admin panel
    

---

## 🔹 **Conclusion**

This lab clearly demonstrates a key security concept:  
If the admin interface is not protected by proper **server-side authorization**, any attacker can access it simply by knowing the path—even without logging in




---
