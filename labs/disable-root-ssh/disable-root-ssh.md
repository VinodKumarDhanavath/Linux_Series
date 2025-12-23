# Disable Direct Root SSH Login on App Servers

## Objective
Enhance server security by preventing direct SSH login as `root`. Users must SSH as a normal user and use `sudo` for administrative tasks.

---

## Servers Targeted
| Server   | User   | Password  | Purpose       |
|----------|--------|-----------|---------------|
| stapp01  | tony   | xxxxxxx   | App Server 1 |
| stapp02  | steve  | xxxxxxx   | App Server 2 |
| stapp03  | banner | xxxxxxx   | App Server 3 |

---

## Manual Steps

### 1️⃣ SSH into the server
```bash
ssh <user>@<server>

###Example :

ssh tony@stapp01
Password: xxxxx

###Confirm Correct Server
hostname

###Edit SSH config
sudo vi /etc/ssh/sshd_config

Enter your user password when prompted.

Find:

#PermitRootLogin yes

Change to:
PermitRootLogin no
Save and exit: ESC :wq ENTER

Validate SSH configuration
sudo sshd -t

No output = configuration syntax correct

Restart SSH service
sudo systemctl restart sshd

Verify root login is blocked
ssh root@localhost

###Output 
Permission Denied

Repeat for all app servers that you want to restric root login.

Example: ssh user@servername

Quick Reference Cheat Sheet

# SSH into server
ssh tony@stapp01

# Edit SSH config
sudo vi /etc/ssh/sshd_config
# Set: PermitRootLogin no

# Validate config
sudo sshd -t

# Restart SSH
sudo systemctl restart sshd

# Verify root login is blocked
ssh root@localhost


Key Points

Only modify target servers.

Direct root SSH is disabled; sudo is used for administrative tasks.

Always validate config (sshd -t) before restarting.

Repeat process server by server if doing manually.

Optional: Use Ansible for multiple servers to automate.

