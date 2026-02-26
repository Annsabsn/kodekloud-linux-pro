Question:
<img width="1863" height="908" alt="Screenshot 2026-02-26 061751" src="https://github.com/user-attachments/assets/d1f080f9-3003-49a3-b14d-735acf0b052b" />
Perfect 👍 You are very close. Follow the exact production-level steps below.

---

# 🎯 Task

Create a user named **`javed`** on **App Server 3** without a home directory.

---

# ✅ STEP-BY-STEP SOLUTION

## 🔹 Step 1: Login to App Server 3 from Jumphost

```bash
ssh banner@stapp03
```

✔ You already confirmed this works.

---

## 🔹 Step 2: Create User Without Home Directory

⚠ Do NOT use `su -`
⚠ Use `sudo`

```bash
sudo useradd -M javed
```

### 🔎 Explanation:

* `sudo` → run command as root
* `useradd` → create user
* `-M` → do NOT create home directory

---

## 🔹 Step 3: Verify User Creation

```bash
id javed
```

OR

```bash
grep javed /etc/passwd
```

---

## 🔹 Step 4: Confirm No Home Directory

```bash
ls /home
```

👉 You should NOT see `javed` folder.

---

# ✅ Final Working Command Flow

```bash
ssh banner@stapp03
sudo useradd -M javed
id javed
```

Click **Check** ✔

---

# 🎯 BASIC INTERVIEW QUESTIONS

### 1️⃣ What does `-M` option do?

👉 Prevents creation of home directory.

---

### 2️⃣ Where is user information stored?

👉 `/etc/passwd`

---

### 3️⃣ Why did `useradd` give “Permission denied”?

👉 Only root can modify `/etc/passwd`.

---

### 4️⃣ Difference between `su` and `sudo`?

| su                  | sudo                       |
| ------------------- | -------------------------- |
| Switch user         | Run single command as root |
| Needs root password | Needs your password        |

---

# 🚀 ADVANCED INTERVIEW QUESTIONS

### 🔥 1️⃣ What files are modified when a user is created?

* `/etc/passwd`
* `/etc/shadow`
* `/etc/group`
* `/etc/gshadow`

---

### 🔥 2️⃣ What happens internally when `useradd` runs?

* Allocates UID
* Updates system account files
* Creates home directory (unless `-M`)
* Assigns default shell

---

### 🔥 3️⃣ How to create system user?

```bash
sudo useradd -r username
```

👉 Used for services (no login).

---

### 🔥 4️⃣ How to create user with no login shell?

```bash
sudo useradd -M -s /sbin/nologin javed
```

---

### 🔥 5️⃣ Difference between service account and normal user?

| Normal User        | Service Account      |
| ------------------ | -------------------- |
| Has login shell    | Usually no login     |
| Has home directory | Often no home        |
| Used by humans     | Used by applications |

---

# 💡 Pro DevOps Tip (Very Important)

For service accounts in production, best practice:

```bash
sudo useradd -r -M -s /sbin/nologin javed
```

More secure 🔐

---
Task Comlection:
<img width="1901" height="890" alt="Screenshot 2026-02-26 062443" src="https://github.com/user-attachments/assets/297cfd35-1d54-486a-b380-47bebcf2a23b" />

