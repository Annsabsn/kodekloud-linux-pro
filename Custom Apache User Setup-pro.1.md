Question :
In response to heightened security concerns, the xFusionCorp Industries security team has opted for custom Apache users for their web applications. Each user is tailored specifically for an application, enhancing security measures. Your task is to create a custom Apache user according to the outlined specifications:

a. Create a user named javed on App server 2 within the Stratos Datacenter. 
b. Assign a unique UID 1880 and designate the home directory as /var/www/javed. explain the question first


Great 👍 You completed it correctly. Let’s break everything clearly and professionally (use this in interviews).

---

# ✅ 1️⃣ Explanation of the Question

### 🔐 What Was the Requirement?

xFusionCorp security team wanted:

* Separate Apache users for each application
* Instead of using a common user like `apache` or `www-data`
* For better security isolation

You were asked to:

1. Create a user named `javed`
2. Do it on **App Server 2**
3. Assign a custom UID `1880`
4. Set home directory as `/var/www/javed`

---

## 🎯 Why This Is Important?

This follows:

* Principle of Least Privilege
* Application isolation
* Prevents cross-application access
* Better permission management

If one application is compromised, attacker cannot access other applications.

---

# ✅ 2️⃣ Explanation of What You Did (Step-by-Step)

From your terminal:

---

## 🔹 Step 1: SSH into App Server 2

```bash
ssh steve@stapp02.stratos.xfusioncorp.com
```

✔ You logged into App Server 2.

---

## 🔹 Step 2: Switch to Root

```bash
sudo su -
```

✔ Required because creating users needs root privileges.

---

## 🔹 Step 3: Create User with Custom UID and Home Directory

```bash
useradd -u 1880 -d /var/www/javed -m javed
```

### 🔎 Command Breakdown

| Option              | Meaning                             |
| ------------------- | ----------------------------------- |
| `useradd`           | Creates new user                    |
| `-u 1880`           | Assigns custom UID                  |
| `-d /var/www/javed` | Sets custom home directory          |
| `-m`                | Creates the directory if not exists |
| `javed`             | Username                            |

✔ This creates:

* User: javed
* UID: 1880
* Home: /var/www/javed
* Directory auto-created

---

## 🔹 Step 4: Verify (Recommended in real world)

```bash
id javed
```

Should show:

```
uid=1880(javed)
```

And:

```bash
ls -ld /var/www/javed
```

---

# ✅ 3️⃣ Why UID 1880?

Normally:

* Linux auto assigns UID (1000+ for normal users)

But here:

* Custom UID ensures no conflict
* Useful in NFS/shared environments
* Required for standardization across servers

---

# ✅ 4️⃣ Security Concept Behind This

Instead of:

```
All apps running as apache
```

We use:

```
App1 → user app1
App2 → user javed
App3 → user app3
```

So file permissions look like:

```
/var/www/javed → owned by javed
```

Other users cannot modify it.

---

# ✅ 5️⃣ Important Interview Questions

### 🔹 Basic Level

1. What is UID in Linux?
2. Difference between UID and GID?
3. What happens if two users have same UID?
4. What is `/etc/passwd`?
5. What does `useradd -m` do?
6. Difference between `useradd` and `adduser`?
7. Why is custom home directory used?

---

# ✅ 6️⃣ Intermediate Interview Questions

1. Why should Apache applications not run as root?
2. How do you disable login for application users?

   ```
   usermod -s /sbin/nologin javed
   ```
3. How do you change ownership of web directory?

   ```
   chown -R javed:javed /var/www/javed
   ```
4. How to assign specific group?

   ```
   useradd -u 1880 -d /var/www/javed -m -g apache javed
   ```

---

# ✅ 7️⃣ Advanced Interview Questions (Very Important 🚀)

### 🔥 Security Focused

1. How does separate Apache user improve security?
2. What is the principle of least privilege?
3. How do you prevent privilege escalation?
4. What is the risk of shared UID across servers?
5. How does SELinux affect Apache users?
6. Difference between system user and normal user?
7. How do you run Apache VirtualHost with different users?
   → Using `suEXEC` or `mpm-itk`

---

### 🔥 DevOps Level

1. How would you automate this user creation?
   → Ansible playbook

2. How to maintain same UID across 100 servers?
   → Centralized directory service (LDAP)

3. What happens if UID conflicts in NFS?
   → Permission mismatch

4. How do containers solve this problem?
   → Namespace isolation

---

# ✅ 8️⃣ Real-World Scenario Question

👉 If an attacker compromises `/var/www/javed`, can they access another app’s files?

Answer:
No, because each app runs under different user and ownership restricts access.

---

# ✅ 9️⃣ How to Explain This Project in Interview

You can say:

> "In this project, I created a custom Apache user with specific UID and home directory to isolate web applications as per security best practices. This ensures application-level isolation and prevents cross-application privilege misuse."

 🧠 Tricky scenario-based questions with answers

Output:
 <img width="1862" height="912" alt="Screenshot 2026-02-20 152308" src="https://github.com/user-attachments/assets/35e33a22-290e-4f5a-8208-9d3a6378abb0" />

