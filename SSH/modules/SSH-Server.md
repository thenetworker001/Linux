The SSH server (`sshd`) listens for incoming connections and handles authentication, session management, and secure communication.

---
The authorised keys to connect to server are stored in: `~/.ssh/authorized_keys` 

---
## Basic Setup

**Install SSH Server**
```bash
sudo apt install openssh-server
```

**Check Service Status**
```bash
sudo systemctl status ssh
```

**Start and Enable Service**
```bash
sudo systemctl start ssh
sudo systemctl enable ssh
```

**Restart Service**
```bash
sudo systemctl restart ssh
```

**Validate Config Before Restart**
```bash
sudo sshd -t
```

**Stop/Disable Server**
Stop (temporary):
```bash
sudo systemctl stop ssh
```

Disable (persist across reboot):
```bash
sudo systemctl disable ssh
```

**Check listening port**
```bash
ss -tulnp | grep ssh
```

Default service port is 22.
If needed change the Service port in config file.

---
## View/Monitor Logs
```bash
sudo journalctl -u ssh --since "1 hour ago"
```

**Live monitoring**
```bash
sudo journalctl -u ssh -f
```
---
## Session Management
**Check logged-in/Active users**
```bash
who
```
**or**
```bash
w
```

**Kill a Session**
```bash
pkill -KILL -t pts/0
```
- `pts/0` = terminal session (Can be found using `who` or `w`)
- Use carefully—this forcefully terminates the session
---
## Firewall and control
**Block connections** (Using Firewall - persistent)
```bash
sudo ufw deny 22
```

**Re-enable connections**
```bash
sudo ufw allow 22
```

**Find Firewall rule**
```bash
sudo ufw status numbered
```

**Delete Firewall rule**
```bash
sudo ufw delete <number>
```

---
## SSH Configuration
Main config file: `/etc/ssh/sshd_config`
Edit/Inspect ssh rules/config for security and other purposes.

---
### Security Hardening

- **Disable root login**
```bash
PermitRootLogin No
```
if can't, Disable password based authentication for root
```bash
PermitRootLogin prohibit-password
```

- **Disable password authentication in config file**
```bash
PasswordAuthentication no
ChallengeResponseAuthentication no
```
Only disable passwords after keys based authentication are working.

- **Use SSH keys only, for authentication (with proper implementation)**

- **Restrict Users**
Allow authorised users only for connection
```bash
AllowUsers yourusername
```
Also restricts the file access for each users at specific level depending on their privilage.

- **Restrict key capabilities**
In `~/.ssh/authorized_keys`:
```bash
command="ls -la",no-port-forwarding,no-X11-forwarding,no-agent-forwarding ssh-ed25519 AAAA...
```
- Limits what that key can do
- Useful for automation or restricted access

- **Change Default port**

- **Use Fail2Ban**
---
---