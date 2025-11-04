# Stage 4 Makefile
# Builds and runs the Python Docker script for Stage 3

IMAGE_NAME=devops-python-script:stage3
STAGE3_DIR=../stage3_python_script_dockerfile
OUTPUT_DIR=$(STAGE3_DIR)/output
API_URL=http://host.docker.internal:5000


# Build Docker image
build:
	docker build -t $(IMAGE_NAME) $(STAGE3_DIR)


# Run /hello mode and save output locally
hello:
	mkdir -p $(OUTPUT_DIR)
	docker run --rm \
		-v $(OUTPUT_DIR):/app/output \
		$(IMAGE_NAME) \
		--mode hello --api-url $(API_URL) --local-file /app/output/hello.txt
