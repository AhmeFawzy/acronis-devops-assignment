FROM python:3.13-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY script.py .

# ENTRYPOINT is fixed as python script.py
ENTRYPOINT ["python", "script.py"]

# Default arguments (optional)
CMD ["--mode", "hello", "--api-url", "http://localhost", "--local-file", "hello.txt"]
