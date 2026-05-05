**SSH**(Secure Shell) is a **cryptographic network protocol** used to securely communicate with another system over an untrusted network.

It provides an **encrypted channel** between a client and a server, ensuring:
- Confidentiality (no one can read the data)
- Integrity (data isn’t tampered with)
- Authentication (you know who you’re talking to)

SSH establishes a secure session that can carry different types of communication.
Over this secure session, you can:
- Execute commands on a remote machine
- Transfer files
- Forward network traffic (tunneling)

SSH is not a shell, a command, or an encryption algorithm.  
It is a network protocol that uses cryptography to securely communicate with a remote system.  
It provides authentication, encryption, and data integrity, and enables tasks such as remote command execution, file transfer, and network tunneling.

---
### Common Use Cases
- **Remote command execution**  
    Run shell commands on another machine
- **Secure file transfer** 
    Using tools like `scp` and `sftp`
- **Port forwarding / tunneling**  
    Route traffic securely through another machine

### Power Features
These are where SSH becomes seriously useful:

- **Local Port Forwarding**  
    Forward a local port to a remote service
- **Remote Port Forwarding**  
    Expose a local service to a remote machine
- **Dynamic Port Forwarding (SOCKS Proxy)**  
    Turn SSH into a proxy (very useful for routing traffic)
- **Background Tunnels**  
    Run SSH sessions without occupying your terminal
- [[File transfer]]  
    Using `scp` / `sftp`
---
### Core Components
SSH works on a **client–server model**:
1. [[SSH-Client]]  
    → The machine initiating the connection
2. [[SSH-Server]]  
    → The machine accepting connections

---
### [[Authentication ]] 
[[Authentication]] is crucial step in the SSH.
SSH supports multiple authentication methods:  
  
- Password-based authentication  
- Key-based authentication (commonly used and more secure when configured properly)  

Additionally, SSH performs **host authentication** using host keys to verify the identity of the server and prevent man-in-the-middle attacks.

---
### Default Port  
  
The SSH server listens on port **22** by default.  
This can be changed in the server configuration (e.g., `sshd_config`).

---
### SSH Setup Overview
To establish a working SSH setup, you typically need:
1. **[[SSH-Server]]**  
   Install and configure the SSH server on the remote machine.
2. **[[SSH-Client]]**  
   Ensure the client machine has an SSH client (usually preinstalled on Linux/macOS).
3. **[[Authentication]]**  
   Choose and configure an authentication method:
   - Password-based authentication  
   - Key-based authentication (recommended)
1. **Connection and Verification**  
   Connect to the server and verify its host key on first connection.
---
---