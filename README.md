# DevOps Assignment - Full Overview

## Overview

This project implements a multi-stage DevOps assignment, including a Flask API server, a Python script, Dockerization, a Makefile, and CI preparation. The goal is to deploy, test, and run a simple REST API with automation, containerization, and command-line execution.

The project is structured into **four stages(So Far)**, each in its own folder.

## Stage 1: API Server (Flask + Ansible)

**Goal:** Implement a simple REST API server and deploy it on a Linux VM.

* **Endpoints:**

  * `GET /hello` → returns `"hello"`
  * `GET /random` → returns a random string
* **Deployment:** Via Ansible playbook to a Linux VM
* **Access:**

  * Locally: `http://127.0.0.1:5000` on the VM
  * Remotely: Using Nginx as a reverse proxy (port 80) and router port forwarding
* **Folder:** `stage1_api_server/`
* **Notes:** Runs in a virtual environment to avoid system-wide package conflicts

---

## Stage 2: Python Script

**Goal:** Create a Python script to interact with the Flask API.

* **Modes:**

  * `hello` → fetch `/hello` and save to a local file
  * `random` → fetch `/random` and save to a remote machine via SSH
* **Dependencies:** `requests`, `paramiko`
* **Folder:** `stage2_python_script/`
* **Usage examples:**

```bash
# Local hello
python script.py --mode hello --api-url http://<VM-IP>:5000 --local-file hello.txt

# Remote random (requires SSH access)
python script.py --mode random --api-url http://<VM-IP>:5000 \
  --remote-host <VM-IP> --remote-user <USER> --remote-password <PASSWORD> --remote-file /home/<USER>/random.txt
```

---

## Stage 3: Dockerization

**Goal:** Wrap the Python script in a Docker container.

* **Docker image:** `devops-python-script:stage3`
* **Usage:**

```bash
# Local hello mode
docker run --rm -v ./output:/app/output devops-python-script:stage3 \
  --mode hello --api-url http://host.docker.internal:5000 --local-file /app/output/hello.txt
```

* **Notes:**

  * Use `host.docker.internal` to access the Flask API running on the host from the container
  * Output files are stored in a mounted `output` directory

---

## Stage 4: Makefile

**Goal:** Automate Docker builds and script execution with simple commands.

* **Makefile targets:**

  * `build` → build the Docker image
  * `hello` → run the script in hello mode and save output locally
* **Usage:**

```bash
# Build Docker image
make build

# Run hello mode (output saved in stage3/output/)
make hello
```
---

