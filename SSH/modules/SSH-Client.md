The SSH client is used to initiate secure connections to an SSH server.

---
### Basic Connection

```bash
ssh user@host
```

This connects to a remote system as `user` at `host` and the [[Authentication]] process is initiated 

---
### Common Options

- **Specify port**
```bash
ssh -p 2222 user@host
```
    
- **Specify identity (private key)**
```bash
ssh -i ~/.ssh/id_ed25519 user@host
```
Even if `-i` is not specified, client automatically tries the available keys in `~/.ssh/`

- **Verbose / debugging output**
```bash
ssh -v user@host      # basic debugssh -vvv user@host    # very detailed debug
```
    
- **Run a single command**
```bash
ssh user@host "ls -la"
```

- **Test a connection**
```bash
ssh -T user@host
```

---
### SSH Config File (Recommended)
Instead of typing full commands every time, you can define shortcuts in:
```bash
~/.ssh/config
```

#### Example:
```bash
Host myserver
    HostName 192.168.1.10
    User kali
    Port 2222
    IdentityFile ~/.ssh/id_ed25519
```

Then simply connect using:
```bash
ssh myserver
```

---
### SSH Agent
The SSH agent is a background process that temporarily holds decrypted private keys, so you don’t have to enter the passphrase every time.

**Start the Agent**
```bash
eval "$(ssh-agent)"
```
> This starts the agent and sets required environment variables for the current shell.

**Add a Key**
```bash
ssh-add ~/.ssh/id_ed25519
```
- You’ll be prompted for the key’s passphrase (if set)
- After that, the key stays unlocked for the session

**List loaded keys**
```bash
ssh-add -l
```

**Remove/Delete key**
```bash
ssh-add -d ~/.ssh/id_ed25519
```
To delete all loaded keys from agent
```bash
ssh-add -D
```

##### Notes:
- The agent runs **per session/environment**  
    → you may need to start it again in a new shell
- If your key has **no passphrase**, the agent adds little security benefit
- The agent does **not store your private key permanently**  
    → it only keeps it in memory while running
---
---