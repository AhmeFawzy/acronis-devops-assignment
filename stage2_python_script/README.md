# Stage 2: Python Script - DevOps Assignment

## Overview

This stage implements a Python script that interacts with the Flask API server from Stage 1.

The script has two modes:

1. **`hello`** – Fetches the `/hello` endpoint and saves the response to a **local file**.
2. **`random`** – Fetches the `/random` endpoint and saves the response to a **remote machine via SSH**.

---

## Requirements

* Python 3.x
* `requests` library
* `paramiko` library

Install dependencies with:

```bash
pip install -r requirements.txt
```

---

## Folder Structure

```
stage2_python_script/
├── script.py
└── requirements.txt
```

---

## Usage

### **1. Local save mode (hello)**

Fetch `/hello` and save locally:

```bash
python script.py --mode hello --api-url http://<FLASK-API-URL> --local-file hello.txt
```

* `<FLASK-API-URL>` → VM IP with Flask/Nginx (e.g., `http://localhost` or `http://<192.168.20.130>`)
* `hello.txt` → local file that will contain the response

Example:

```bash
python script.py --mode hello --api-url http://localhost --local-file hello.txt
```

---

### **2. Remote save mode (random)**

Fetch `/random` and save to remote VM via SSH:

```bash
python script.py --mode random --api-url http://<FLASK-API-URL> --remote-host <VM-IP> --remote-user <USER> --remote-password <PASSWORD> --remote-file /home/<USER>/random.txt
```

Example:

```powershell
python script.py --mode random --api-url http://localhost --remote-host 192.168.20.130 --remote-user ahmed --remote-password YourVMPassword --remote-file /home/ahmed/random.txt
```

* SSH login required for remote machine
* Check remote file:

```bash
ssh ahmed@192.168.20.130
cat /home/ahmed/random.txt
```

---

## Testing in our setup

1. **Flask API is running on the VM**, accessible via Nginx port 80.
2. **Local mode:**

   * Script fetches `/hello` and writes to `hello.txt` on Windows host.
3. **Remote mode:**

   * Script fetches `/random` and saves to `/home/ahmed/random.txt` on VM via SSH.
4. Both modes tested successfully using local host URL and VM SSH.

---

## Notes

* Ensure Flask API is running before executing the script.
* Use PowerShell single-line command if running on Windows.
