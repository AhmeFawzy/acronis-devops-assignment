# Stage 3: Dockerized Python Script - DevOps Assignment

## Overview

This stage wraps the Stage 2 Python script in a Docker container. The container supports two modes:

1. **`hello`** – Fetch `/hello` from the Flask API and save locally.
2. **`random`** – Fetch `/random` from the Flask API and save to a remote VM via SSH key.

The Docker image includes all dependencies, so you only need to specify the mode and parameters.

---

## Build the Docker Image

```bash
docker build -t devops-python-script:stage3 .
```

---

## Usage

### 1. Hello Mode (Local File)

Create an output folder on your host:

```bash
mkdir -p output
```

Run the container:

```bash
docker run --rm -v ${PWD}/output:/app/output devops-python-script:stage3 \
  --mode hello \
  --api-url http://host.docker.internal:5000 \
  --local-file /app/output/hello.txt
```

* The file `hello.txt` will appear in `stage3_python_script_dockerfile/output/`.

---

### 2. Random Mode (Remote File via SSH Key)

Run the container and save `/random` to a remote VM:

```bash
docker run --rm -v ~/.ssh/id_rsa:/root/.ssh/id_rsa:ro devops-python-script:stage3 \
  --mode random \
  --api-url http://host.docker.internal:5000 \
  --remote-host <VM-IP> \
  --remote-user <USER> \
  --ssh-key /root/.ssh/id_rsa \
  --remote-file /home/<USER>/random.txt
```

* Replace `<VM-IP>` and `<USER>` with your VM details.
* Ensure passwordless SSH login using the mounted key.
* Verify the file on the VM:

```bash
ssh <USER>@<VM-IP>
cat /home/<USER>/random.txt
```

---

## Notes

* Use `host.docker.internal` to reach the Flask API running on your host/VM.
* Mount a local folder to persist files written by the container.
* `--rm` ensures the container is ephemeral.
* The SSH key must have proper permissions (`chmod 600 ~/.ssh/id_rsa`).
