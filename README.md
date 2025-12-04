# SYSTEM ADMINISTRATOR

## sudo – Super User Do
- The special key is `sudo`, which temporarily grants you permission to perform an action that requires elevated privileges.

### Feature Comparison Table

    | Feature            | root       | sudo                       |
    |-------------------|------------|----------------------------|
    | Is it a user?      | Yes        | No (it's a command)        |
    | Unlimited power?   | Yes        | Yes, but temporarily       |
    | Security           | Risky      | Safer                      |
    | Logging of actions | No         | Yes                        |
    | Can be restricted? | No         | Yes (sudoers file)         |
    | Typical use        | System admin | Regular users doing admin tasks |

## SSH Key-Based Authentication

SSH (Secure Shell) is a secure way to connect to another computer over a network.

### How SSH Works (Simple Explanation)

SSH uses two keys:

- 🔐 **Private Key** – stays on your computer  
- 🔓 **Public Key** – you upload it to server / cloud / GitHub / Azure DevOps

When you connect:

1. Server checks your public key.
2. Server sends a challenge that only your private key can answer.
3. If the answer matches → **You are authenticated (logged in).**
4. **Password is NOT required.**

> **Private key must never be shared.**  
> **Public key can be shared with anyone.**

1.To create the SSH key;

    ssh-keygen -t rsa -b 4096 -C "name@gmail.com
    |           |  |      |        └── comment (email/identifier)   
    |           |  |      |
    |           |  |      └── bit size (key strength)
    |           |  |       
    |           |  |
    |           |  |
    |           |  └── algorithm type
    |           └── type of key to create 
    |
    └── type of key to create

2. It asks a file location  
3. It asks for a passphrase (optional)

File Paths:
  /.ssh/id_rsa.pub # public key
  /.ssh/id_rsa # private key


## How to Add SSH Key to Azure DevOps

1. Go to **Azure DevOps → Top right User Settings**
2. Click **SSH Public Keys**
3. Click **Add Key**
4. Paste the content of the **public key** there → **Save**

#with this ssh authentication ,no password is needed

FLOW OF SSH AUTHENTICATES:

    Client (your laptop)        Server (Azure/Git/VM)
    --------------------------------------------------------
    1.Sends request          --->    Checks if your PUBLIC key exists
    2.Server sends challenge <--- Needs private key to decode
    3.Client uses PRIVATE key to reply
    4.Server confirms match  --->  Access granted (login success)

# USER AND GROUP MANAGEMENT:

User and group management refers to creating, modifying, and controlling:

### Users  
People or system accounts that can log in.

### Groups  
Collections of users who share permissions.

### Permissions  
What a user/group can read (r-4), write (w-3), or execute (x-1).

---

## USERS:

![Image](image/image1.png)

### To create the user  




