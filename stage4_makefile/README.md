## **Stage 4: Makefile - DevOps Assignment**

### **Overview**

This stage provides a **Makefile** to build and run the Python Docker script from Stage 3.

* Currently supports **hello mode** only.
* Fetches `/hello` from the Flask API and saves it locally.
* Random mode (SSH to remote host) is temporarily disabled for safety.

---

### **Usage**

1. **Build Docker image**:

```bash
make build
```

2. **Run hello mode**:

```bash
make hello
```

* Fetches `/hello` from the Flask API.
* Saves the response to the path specified in the Makefile (inside Stage 3 Docker folder by default).

---

### **Notes**

* Ensure Stage 3 Docker folder (`../stage3_python_script_dockerfile`) contains:

  * `script.py`
  * `requirements.txt`
  * `Dockerfile`

* Docker container uses `host.docker.internal` to connect to the Flask API running on your host/VM.
