# Linux User & Permission Management Task  


# User and File Permission Setup

## Task Overview
This document provides a step-by-step guide on how users were created and file permissions were configured on a Linux virtual machine.

## 1. Creating the Tupu User
We used the `adduser` script to create the `tupu` user, which automatically set up the user profile, home directory, and default user group.
```bash
sudo adduser tupu
```

## 2. Creating the Lupu User
We used the `useradd` command with specific flags to ensure that `lupu` had a home directory, a user profile, and a user group.
```bash
sudo useradd -m -d /home/lupu -s /bin/bash -G lupu lupu
```

## 3. Creating the Hupu System User
Since `hupu` is a system user with no login capabilities, we used the following command:
```bash
sudo useradd --system --shell /bin/false hupu
```

## 4. Adding Users to the Sudo Group
There are two methods to grant `tupu` and `lupu` sudo privileges:

### Method 1: Editing the sudoers file via visudo
```bash
sudo visudo
```
Add the following lines at the end of the file:
```
tupu ALL=(ALL:ALL) ALL
lupu ALL=(ALL:ALL) ALL
```

### Method 2: Adding Users to the sudo Group
```bash
sudo usermod -aG sudo tupu
sudo usermod -aG sudo lupu
```

## 5. Setting Up /opt/projekti Directory with Proper Permissions
We created the `/opt/projekti` directory and set up a group that allows only `tupu` and `lupu` to access and modify the files.

### Step 1: Create the `projekti` Group
```bash
sudo groupadd projekti
```

### Step 2: Add Users to the Group
```bash
sudo usermod -aG projekti tupu
sudo usermod -aG projekti lupu
```

### Step 3: Change Ownership of the Directory
```bash
sudo mkdir -p /opt/projekti
sudo chown :projekti /opt/projekti
```

### Step 4: Set Proper Permissions
```bash
sudo chmod 2770 /opt/projekti
```
- `2` sets the SetGID bit, ensuring that new files inherit the `projekti` group.
- `770` allows full access to group members and denies access to others.

## Conclusion
This setup ensures that only `tupu` and `lupu` can access and modify files in `/opt/projekti`, while `hupu` remains a system user without login capabilities. The sudo privileges for `tupu` and `lupu` were configured successfully.
