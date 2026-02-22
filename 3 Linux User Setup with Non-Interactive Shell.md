Question:


<img width="813" height="897" alt="Screenshot 2026-02-22 145009" src="https://github.com/user-attachments/assets/a4eafca5-8aad-453d-937c-cc29cdcdc23f" />
Great ✅ You have successfully created the user **jim** with a non-interactive shell.

Now I’ll explain **what you did step-by-step**, then provide **interview questions + advanced questions** (since you’re preparing for DevOps/Linux interviews).

---

# ✅ Step-by-Step Explanation of What You Did

### 🔹 1️⃣ SSH into App Server 2

```bash
ssh steve@stapp02
```

* Connected from jumphost to **App Server 2 (stapp02)**.
* First-time connection → SSH asked to verify host fingerprint.
* You typed `yes` → Host key stored in `~/.ssh/known_hosts`.

---

### 🔹 2️⃣ Switch to Root User

```bash
sudo -i
```

* Switched to root user.
* Required because **creating users needs root privileges**.
* System showed sudo security reminder.

---

### 🔹 3️⃣ Create User with Non-Interactive Shell

```bash
useradd -s /sbin/nologin jim
```

### 🔎 What this command does:

| Option          | Meaning                    |
| --------------- | -------------------------- |
| `useradd`       | Creates a new user         |
| `-s`            | Specifies login shell      |
| `/sbin/nologin` | Prevents interactive login |
| `jim`           | Username                   |

✔ This creates:

* Home directory entry `/home/jim`
* Default UID & GID
* Shell set to `/sbin/nologin`

---

### 🔹 4️⃣ Incorrect Command (Minor Mistake)

```bash
getent passwd | jim
```

❌ Error:

```
-bash: jim: command not found
```

👉 Because `| jim` tries to execute `jim` as a command.

---

### 🔹 5️⃣ Correct Verification Command

```bash
getent passwd | grep jim
```

Output:

```
jim:x:1002:1002::/home/jim:/sbin/nologin
```

### 🔎 Meaning of Output Fields:

```
username:password:UID:GID:comment:home:shell
```

For jim:

* Username → jim
* UID → 1002
* Home → /home/jim
* Shell → /sbin/nologin ✅ (Non-interactive confirmed)

---

# 🎯 Final Result (Task Completed)

✔ User `jim` created
✔ Shell set to `/sbin/nologin`
✔ User cannot log in
✔ Verified in `/etc/passwd` via `getent`

---

# 🔥 Interview Questions (Basic – DevOps/Linux)

### 1️⃣ What is the difference between `useradd` and `adduser`?

**Answer:**

* `useradd` → Low-level binary command
* `adduser` → Friendly Perl script (more interactive)

---

### 2️⃣ What is a non-interactive shell?

A shell like `/sbin/nologin` or `/bin/false` that prevents user login.

---

### 3️⃣ Where are user details stored in Linux?

In:

```
/etc/passwd
/etc/shadow
/etc/group
```

---

### 4️⃣ What is the purpose of `/etc/shadow`?

Stores encrypted passwords and password aging info.

---

### 5️⃣ What does `getent passwd` do?

Fetches user information from NSS (local files, LDAP, etc.).

---

# 🚀 Advanced Interview Questions

### 🔥 1️⃣ What is the difference between `/bin/false` and `/sbin/nologin`?

| `/bin/false`      | `/sbin/nologin`                                         |
| ----------------- | ------------------------------------------------------- |
| Immediately exits | Shows message "This account is currently not available" |
| No message        | Better for service accounts                             |

---

### 🔥 2️⃣ How would you modify an existing user's shell?

```bash
usermod -s /sbin/nologin username
```

---

### 🔥 3️⃣ How do you lock a user account without deleting it?

```bash
usermod -L username
```

OR

```bash
passwd -l username
```

---

### 🔥 4️⃣ How do you create a system user for services?

```bash
useradd -r -s /sbin/nologin serviceuser
```

`-r` → Creates system account (low UID)

---

### 🔥 5️⃣ How does SSH prevent unknown host attacks?

It stores host fingerprint in:

```
~/.ssh/known_hosts
```

Prevents Man-in-the-Middle attacks.

---

### 🔥 6️⃣ What happens internally when you run `useradd`?

It:

* Updates `/etc/passwd`
* Updates `/etc/shadow`
* Creates group in `/etc/group`
* Optionally creates home directory
* Assigns UID & GID

---

# 🏆 Pro DevOps Tip

For automation (Ansible / scripts), always use:

```bash
useradd -r -s /sbin/nologin -m jim
```

Because:

* `-r` → system account
* `-m` → creates home directory

---
Execute:
<img width="1863" height="907" alt="Screenshot 2026-02-22 145025" src="https://github.com/user-attachments/assets/051d0034-bae4-496d-90f2-1c09a775b572" />
------------------------------------------------------------------------------------------------------------------------------------------------------------------
Complection:
<img width="1859" height="906" alt="Screenshot 2026-02-22 145048" src="https://github.com/user-attachments/assets/b4a51848-4b83-413d-b753-be54a29d2357" />
