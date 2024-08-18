
---

# Installing MongoDB 7.0 Community Edition on Ubuntu

This guide will help you install MongoDB 7.0 Community Edition on Ubuntu 20.04 LTS ("Focal") and Ubuntu 22.04 LTS ("Jammy"). MongoDB 7.0 supports 64-bit versions of these platforms.

## Prerequisites

Ensure your system meets the following requirements:
- 64-bit version of Ubuntu 20.04 LTS or 22.04 LTS.
- Access to a terminal with `sudo` privileges.

## Determine Your Ubuntu Version

To check your Ubuntu version, run:
```bash
cat /etc/lsb-release
```

## Step-by-Step Installation

### 1. Install Required Packages

First, make sure `gnupg` and `curl` are installed:
```bash
sudo apt-get install gnupg curl
```

### 2. Import the MongoDB Public GPG Key

Import the MongoDB public GPG key:
```bash
curl -fsSL https://www.mongodb.org/static/pgp/server-7.0.asc | \
   sudo gpg -o /usr/share/keyrings/mongodb-server-7.0.gpg --dearmor
```

### 3. Create the MongoDB List File

Create the MongoDB repository list file. Replace `jammy` with `focal` if you are using Ubuntu 20.04.

For Ubuntu 22.04 (Jammy):
```bash
echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-7.0.gpg ] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/7.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-7.0.list
```

For Ubuntu 20.04 (Focal):
```bash
echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-7.0.gpg ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/7.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-7.0.list
```

### 4. Reload Local Package Database

Update the local package database:
```bash
sudo apt-get update
```

### 5. Install MongoDB

Install MongoDB with the following command:
```bash
sudo apt-get install -y mongodb-org
```

### 6. Start MongoDB

Start the MongoDB service:
```bash
sudo systemctl start mongod
```

If you encounter an error such as `Failed to start mongod.service: Unit mongod.service not found.`, reload the systemd manager configuration:
```bash
sudo systemctl daemon-reload
```
Then try starting MongoDB again:
```bash
sudo systemctl start mongod
```

### 7. Verify MongoDB Status

Check if MongoDB is running successfully:
```bash
sudo systemctl status mongod
```

### 8. Enable MongoDB to Start on Boot

Optionally, ensure MongoDB starts automatically at system boot:
```bash
sudo systemctl enable mongod
```

### 9. Stop MongoDB

To stop the MongoDB service:
```bash
sudo systemctl stop mongod
```

### 10. Restart MongoDB

To restart the MongoDB service:
```bash
sudo systemctl restart mongod
```

## Troubleshooting

If you encounter issues, consult the MongoDB [documentation](https://www.mongodb.com/docs/manual/administration/install-on-linux/) or check the service logs for more details.

---

