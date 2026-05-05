Authentication is a core part of SSH security.

It ensures:
- **Authentication** → verifying identities
- **Confidentiality** → encrypting communication
- **Integrity** → preventing data tampering

SSH performs **two separate authentication processes**:
1. **Client Authentication** → server verifies the user
2. **Host Authentication** → client verifies the server
---
## Client Authentication
The server verifies that the connecting user is legitimate.

### Methods
#### 1. Password-Based Authentication
- The client is prompted for the user’s password on the remote system
- Simple but weaker:
    - Vulnerable to brute-force attacks
    - Often disabled on hardened systems
#### 2. SSH Key-Based Authentication
A cryptographic key pair is used instead of a password.
- **Private key** → stays on the client (must be kept secure)
- **Public key** → stored on the server

Server authenticates the client by:
- **A challenge–response mechanism**
- The client proves it owns the private key by signing data
- The server verifies this using the public key


**Generate SSH Keys** (On Client)
```bash
ssh-keygen -t ed25519
```
Creates:
- `~/.ssh/id_ed25519` (private key)
- `~/.ssh/id_ed25519.pub` (public key)

- Use `-C` to add comment which will be added at the last part of public key to identify the file easily.

**Copy Public Key to Server**
Using existing access:
```bash
ssh-copy-id user@server_ip
```

Or manually:
- Copy contents of `.pub` file
- Paste into:
```bash
~/.ssh/authorized_keys
```
on server.

**Remove Old Host Entry**
Removes host from know host list
```bash
ssh-keygen -R host
```

##### SSH Key Hardening
If properly handled, SSH key are secure than password
- Use `edt25519` algorithm instead of `rsa` if compatible
- Private key should have restricted permissions:
```bash
chmod 600 ~/.ssh/id_ed25519
```
- Always use **passphrase** for better security
- Never share your private key
- Backup keys safely and securely
- Use different keys for different purposes
---
### Host Authentication
The client verifies that it is connecting to the correct server.

**How It Works**
- Each server has a unique **host key**
- On first connection, SSH shows a fingerprint:
```bash
The authenticity of host 'example.com' can't be established...
```
- If accepted:
     The key is stored in:
```bash
~/.ssh/known_hosts
```

- On Future Connections SSH compares the server’s key with the stored one. Any mismatch triggers a security warning.

---
---