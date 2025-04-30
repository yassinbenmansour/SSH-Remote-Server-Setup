# Linux Server Setup with SSH Key Authentication

##  Project Goal

The goal of this project is to learn and practice the basics of Linux, particularly remote server setup and secure SSH access using key pairs.

---

##  What Was Done

-  Created and configured a remote Linux server (Ubuntu 24.10).
-  Generated two separate SSH key pairs.
-  Added both public keys to the server.
-  Verified access using both private keys.
-  Configured the SSH client for easy access via aliases.

---

## ☁️ Step 1: Set Up Remote Linux Server

Used [DigitalOcean](https://digitalocean.com) to create a simple droplet:

- OS: Ubuntu 24.10 x64
- Plan: Basic
- Login as `root` (initially using password or SSH key)

---

##  Step 2: Generate Two SSH Key Pairs Locally

On your local machine:

```bash
ssh-keygen -t ed25519 -f ~/.ssh/key1
ssh-keygen -t ed25519 -f ~/.ssh/key2
```

##  Step 3: Add Public Keys to Remote Server

To allow the server to authenticate using your SSH keys, you need to copy the public keys to the server.

1. **Connect to your server** as `root` using your password or the default SSH key:

   ```bash
   ssh root@<your-server-ip>

- Then:
   ```bash
    mkdir -p ~/.ssh
    nano ~/.ssh/authorized_keys
    ```
Paste the contents of key1.pub and key2.pub, one per line.

- Then:
  
  ```bash
    chmod 600 ~/.ssh/authorized_keys
    chmod 700 ~/.ssh
    exit
    ```

##  Step 4: Test SSH Connection Using Both Keys

1. **From your local machine:**:

    ssh -i ~/.ssh/key1 root@<server-ip>
    ssh -i ~/.ssh/key2 root@<server-ip>

## 5. Configure `~/.ssh/config` for Easy Access

To simplify SSH access, you can create an SSH configuration file on your local machine. This allows you to connect to your server using aliases instead of typing the full command each time.

### Steps:

1. **Edit your local SSH config file**:
   Open the SSH configuration file located at `~/.ssh/config`:
   ```bash
   nano ~/.ssh/config

   ```ini
    Host server1-key
    HostName server-ip
    User root
    IdentityFile ~/.ssh/key1

    Host server1-key2
        HostName server-ip
        User root
        IdentityFile ~/.ssh/key2

### Now, you can log into your server using either of the following commands:

- To connect using the first SSH key (`key1`):
  ```bash
  ssh server1-key1
