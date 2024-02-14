# NCAE

## Installation
```bash
git clone https://github.com/loganflecke/NCAE.git
```
or
```bash
wget https://github.com/loganflecke/NCAE/archive/refs/heads/main.zip
tar xvf main.zip
```

## Usage
1. Select the file based on your OS (CentOS/RHEL or Debian/Ubuntu)
2. ```bash
   chmod 755 harden_[centos/debian]
   ```
3. ```bash
   sudo ./harden_[centos/debian]
   ```

## Analysis
1. Read the `harden.txt` file that was just created
2. Check the Shadow file and Passwd file for unnecessary users
3. Ensure only root user has full sudo permissions
4. Check cron jobs
5. Check files with SUID or SGID permissions against the known exploits at [GTFOBins SUID](https://gtfobins.github.io/#+suid)
6. Check files and directories that any user can write to (world-writable files and directories)
7. Remove unnecessary services in `/etc/systemd/system` and `/etc/systemd/user` with ```sudo systemctl stop <service>``` or ```sudo apt/yum remove <service>```
8. Use Auditd to monitor activity on this endpoint

## Auditd
Get a brief report of events on the machine:
```bash
aureport
```
Query various events on the machine:
```bash
ausearch -m <message>
```

Useful messages:
1. `USER_AUTH`: User authentication events.
2. `CRED_ACQ`: Credential acquisition events.
3. `USER_CMD`: User command execution events.
4. `CONFIG_CHANGE`: Configuration change events.
5. `CRYPTO_KEY_USER`: User-level cryptographic key events.

