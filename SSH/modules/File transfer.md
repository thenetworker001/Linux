///////////////   (unfinished)  /////////////////////

File transfer can be securely done via SSH using different applications and methods:

SCP:
Upload file:
```bash
scp file.txt usr@host:/home/user/
```
Download file:
```bash
scp user@host:/path ./directory
```
Copy directories: use `-r`
 Reality of `scp`
- ✔️ Simple
- ❌ Not efficient
- ❌ No resume support
- ❌ Minimal features

use rsync:
Upload:
```bash
rsync -avz file.txt user@host:/home/user/
```
Download:
```bash
rsync -avz user@host:/home/user/file.txt .
```
sync folder:
```bash
rsync -avz folder/ user@host:/home/user/folder/
```

SFTP