#  PortSwigger: User Role Controlled by Request Parameter

## 🔹 Lab Information

- **Lab Name:** User role controlled by request parameter
- **Level:** 3
- **Vulnerability Type:**
    
    - Broken Access Control
    - Privilege Escalation
    - Cookie Manipulation
        

---

## 🔹 Vulnerability Description

The issue in this lab is that the application determines whether a user is an **admin or a normal user** using a **forgeable cookie**.

If the cookie contains:

`Admin=false`

you’re a normal user.  
But if you change it to:

`Admin=true`

you immediately become an admin — without any server-side validation.

This is a critical security flaw because it allows attackers to escalate their privileges simply by modifying a cookie value.

---

## 🔹 Exploitation Steps

### **1) Attempt to Access the Admin Panel**

I visited:

`/admin`

and received an "access denied" message, confirming I'm not an admin.

---

### **2) Log in Using the Provided Credentials**

Used:

`username: wiener password: peter`

With Burp Suite running, interception of **responses** was enabled.

---

### **3) Modify the Cookie in the Response**

In the server response, the application sets the cookie:

`Admin=false`

I modified it to:

`Admin=true`

and forwarded the response.

---

### **4) Access the Admin Panel**

After the modification, visiting:

`/admin`

successfully opened the admin interface.

---

### **5) Delete User “carlos”**

Inside the admin panel, I selected the user:

`carlos`

Clicked **Delete**, and the account was removed.

---

## 🔹 Security Impact

This vulnerability is **critical**, allowing any standard user to become an admin by altering a cookie.

An attacker could:

- Modify or delete user accounts
    
- Access sensitive information
    
- Perform administrative actions
    
- Potentially take full control of the system
    

---

## 🔹 Root Cause

- Storing user privileges directly in a cookie
    
- No server-side validation of authorization
    
- Weak access control design
    
- Easily forgeable parameters
    

---

## 🔹 How to Fix

✔ Do not store privilege levels directly in cookies  
✔ Use server-side session-based authorization  
✔ Implement signed or encrypted tokens  
✔ Validate permissions on every privileged request  
✔ Protect admin endpoints from unauthorized users

---

## 🔹 Evidence

- Cookie returned as: `Admin=false`
   `Put here image`
- Changed to: `Admin=true`
   `Put here image`
- Admin panel accessible after modification
   `Put here image`
- Successfully deleted user **carlos**
   `Put here image`
    

---

## **Conclusion**

The root issue is storing authorization levels in a client-side cookie.  
By modifying a single value, attackers can escalate privileges and gain full administrative control.
