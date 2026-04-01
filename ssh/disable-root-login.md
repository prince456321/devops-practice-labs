##  Disable Root Login
#### After doing some security audits of servers, xFusionCorp Industries security team has implemented some new security policies. One of them is to disable direct root login through SSH. Disable direct SSH root login on all app servers in Stratos Datacenter.
### Click on ✔ and Do Task Again
### Solution:-

### Step 1: Open SSH Sessions to All App Servers
Open Three terminals. Ensure you have the passwords ready (usually provided in the lab details).
- App Server 1  ```ssh tony@stapp01```
- App Server 2  ```ssh steve@stapp02```
- App Server 3  ```ssh banner@stapp03```

### Step 2: Edit the SSH Configuration on each app server and Search for #PermitRootLogin
```sh
sudo vi /etc/ssh/sshd_config
# In vi editor, search for the line by typing:
# Press '/' then type 'PermitRootLogin' and press Enter
/PermitRootLogin

# You'll find one of these configurations:
# - #PermitRootLogin yes                    (commented out, root login allowed)
# - #PermitRootLogin prohibit-password      (commented out, password auth disabled)
# - PermitRootLogin yes                     (active, root login allowed)

# To edit:
# 1. Press 'i' to enter INSERT mode
# 2. Remove the '#' symbol if present
# 3. Change the value to 'no'
# 4. Press 'Esc' to exit INSERT mode
# 5. Type ':wq' and press Enter to save and quit

# Correct configuration should look like:
# PermitRootLogin no
```
![image](https://lh6.googleusercontent.com/zslcgqljknsN65REyHnq2ZQEV26IWMBlq0ZsbUpc6mILAl-iYASnJ4uAH5nNzaz-QCtPFXoV1LqTPbvAQ_W6acgpo7x5cUdlSny09UiYoQJQe5uot0L8u95OcotvD1lHGmZ0rHw2)

### Step 3: Verify the Configuration
Check for syntax errors:
```sh
sudo sshd -t
```
If no errors are displayed, the configuration is valid.

### Step 4: Restart SSH Service
Apply the changes by restarting the SSH daemon:

```sh
sudo systemctl restart sshd
```
### Step 5: Verify SSH Service Status
Confirm the service restarted successfully:
```sh
sudo systemctl status sshd
```
### Step 6: Verify Configuration File
Confirm the change persists:
```sh
sudo grep "^PermitRootLogin" /etc/ssh/sshd_config
```
Expected output: ```PermitRootLogin no```

### Step 7: Test the Configuration
Important: Keep your current SSH session open while testing.

Open a new terminal and attempt to connect as root:
```sh
ssh root@stapp01
```
You should receive: "Permission denied" or "Access denied"

