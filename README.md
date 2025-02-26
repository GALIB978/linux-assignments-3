# Linux User & Permission Management Task  


# User and File Permission Setup


## 1. Creating the Tupu User
We used the `adduser` script to create the `tupu` user
- Command used : `sudo adduser tupu`

## 2. Creating the Lupu User
We used the `useradd` command for `lupu` with similar properties
- Command used : `sudo useradd -m -d /home/lupu -s /bin/bash -G lupu lupu`

## 3. Creating the Hupu System User
Since `hupu` is a system user with no login capabilities

- Command used : `sudo useradd --system --shell /bin/false hupu`

## 4. Adding Users to the Sudo Group
There are two methods to grant `tupu` and `lupu` sudo privileges:

### Method 1: Editing the sudoers file via visudo

- `sudo visudo`
Add the following lines at the end of the file:

- tupu ALL=(ALL:ALL) ALL
- lupu ALL=(ALL:ALL) ALL


### Method 2: Adding Users to the sudo Group

- sudo usermod -aG sudo tupu
- sudo usermod -aG sudo lupu



## 5. Setting Up /opt/projekti Directory with Proper Permissions
We created the `/opt/projekti` directory and set up a group that allows only `tupu` and `lupu` to access and modify the files.

### Step 1: Create the `projekti` Group

- Command used : `sudo groupadd projekti`

### Step 2: Add Users to the Group
- Command used : 
- `sudo usermod -aG projekti tupu`
- `sudo usermod -aG projekti lupu`


### Step 3: Change Ownership of the Directory
- Command used :
- `sudo mkdir -p /opt/projekti`
- `sudo chown :projekti /opt/projekti`


### Step 4: Set Proper Permissions

- Command used : `sudo chmod 2770 /opt/projekti`

- `2` sets the SetGID bit, ensuring that new files inherit the `projekti` group.
- `770` allows full access to group members and denies access to others.

## Conclusion
This setup ensures that only `tupu` and `lupu` can access and modify files in `/opt/projekti`, while `hupu` remains a system user without login capabilities. The sudo privileges for `tupu` and `lupu` were configured successfully.
