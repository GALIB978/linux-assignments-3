# Linux User & Permission Management Task  

## **1. Introduction**  
This task involved creating users, managing permissions, and setting up a secure directory using Linux commands. Below is the step-by-step guide on how the task was completed.  

---

## **2. Steps Followed**  

### **Step 1: Create Tupu User**  
Command:  
```bash
sudo adduser tupu
This command creates the user tupu with a home directory and necessary configurations.

Step 2: Create Lupu User
Command:

bash
Copy
Edit
sudo useradd -m -d /home/lupu -s /bin/bash -G lupu lupu
This command creates the lupu user with:

A home directory (/home/lupu)
The default shell (/bin/bash)
A group named lupu
Step 3: Create Hupu System User
Command:

bash
Copy
Edit
sudo useradd --system --shell /bin/false hupu
This creates a system user hupu that cannot log in since its shell is set to /bin/false.

Step 4: Add Users to Sudo Group
Commands:

bash
Copy
Edit
sudo usermod -aG sudo tupu
sudo usermod -aG sudo lupu
This grants administrative privileges to tupu and lupu.

Step 5: Secure /opt/projekti Directory
Commands:

bash
Copy
Edit
sudo mkdir -p /opt/projekti
sudo groupadd projekti
sudo usermod -aG projekti tupu
sudo usermod -aG projekti lupu
sudo chown :projekti /opt/projekti
sudo chmod 2770 /opt/projekti
Explanation:

Created the directory /opt/projekti.
Created a new group projekti.
Added tupu and lupu to the projekti group.
Changed the group ownership of /opt/projekti to projekti.
Set permissions 2770, meaning:
Only projekti group members can read, write, and execute.
Newly created files inherit the projekti group ownership.

