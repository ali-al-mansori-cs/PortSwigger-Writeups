# PortSwigger: Unprotected admin functionality with unpredictable URL

## 🔹 Lab Information

- **Lab Name:** Unprotected admin functionality with unpredictable URL
- **Level:** 2
- **Vulnerability Type:**
    
    - Broken Access Control  
    - Unprotected Admin Panel 
    - Information Disclosure (sensitive admin path leaked in JavaScript)
        

---

## 🔹 Vulnerability Description

The issue in this lab is that the admin panel is placed at an **unpredictable, hidden URL**, but it is **not protected** by any authentication or authorization checks.  
Although the admin path is not publicly shown, it is accidentally **disclosed through JavaScript code** on the homepage.

This makes the admin panel accessible to anyone who discovers the hidden path, allowing attackers to perform critical administrative actions.

---

## 🔹 Step-by-Step Exploitation

### **1) Inspecting the Home Page Source**

I opened the homepage and inspected the source code using the browser’s developer tools or Burp Suite.

Inside the inline JavaScript code, I found a variable containing the admin panel path:

`var adminPanel = "/admin-8f3a9b";`

This reveals the hidden admin URL.

---

### **2) Accessing the Admin Panel**

After identifying the path, I accessed the admin panel directly:

`/admin-8f3a9b`

The page loaded **without requiring any login**, confirming a lack of authorization controls.

---

### **3) Deleting the user “carlos”**

Inside the admin interface, I found the user list.  
I selected the user:

`carlos`

Then clicked **Delete**.  
The user account was removed successfully.

---

## 🔹 Impact

This vulnerability is **critical** because it allows any attacker to:

- Access the admin panel without authentication
    
- Delete or modify user accounts
    
- Access sensitive data
    
- Take full control of the application
  

---

## 🔹 Root Cause

- Missing server-side authorization checks
    
- Relying on “hidden URLs” instead of proper access control
    
- Exposing sensitive paths in client-side JavaScript
    
- Weak or nonexistent access control mechanisms
    

---

## 🔹 Fix Recommendations

✔ Implement strict **server-side authorization** on all admin endpoints  
✔ Do **not** expose sensitive URLs in JavaScript or client-side code  
✔ Use role-based access control (RBAC)  
✔ Ensure admin pages require a valid authenticated session  
✔ Add monitoring and logging for suspicious access attempts

---

## 🔹 Evidence

- Admin URL found in JavaScript source
              `Put here image`
    
- Admin panel accessible without authentication
               `Put here image`
    
- Successful deletion of user **carlos**
               `Put here image`
    

---

# Conclusion

The core issue is exposing a hidden but **unprotected** admin panel.  
Even though the URL was unpredictable, leaking it through JavaScript made it discoverable and accessible, enabling full administrative actions without any authorization
