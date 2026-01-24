Got it 😄 — keeping it **straightforward and practical**, no fluff.
# Installing the AppDynamics Python Agent (Docker)

## Prerequisites

* Docker image running a Python application
* AppDynamics Python Agent package or pip access
* AppDynamics Controller details (host, port, account, access key)

---

## Installation Steps

### 1. Access the Running Container (Optional)

If you need to validate or troubleshoot inside a running container:

```bash
docker exec -it <container_name> bash
```

---

### 2. Install the AppDynamics Python Agent

Using **pip**:

```bash
pip install appdynamics
```

Or, if you have the agent package locally:

```bash
tar -xjf appdynamics-pythonagent-25.x.x.tar.bz2
pip install appdynamics-pythonagent-xxx.whl
```

---

### 3. Create the Controller Configuration File

Create a file named `controller_info.cfg`.

Example:

```ini
[agent]
app = PyAgent
tier = t1
node = n1

[controller]
host = 192.168.1.121
port = 8090
account = customer1
accesskey = your_access_key
```

---

### 4. Run the Application Using the Python Agent

Start the application through the AppDynamics agent wrapper.

Example using **Gunicorn**:

```bash
pyagent run -c path_to/controller_info.cfg -- gunicorn -w 4 -b 0.0.0.0:8000 project.wsgi:application
```

---

## Example Dockerfile

```dockerfile
# Use official Python 3.13 slim image
FROM python:3.13-slim

# Environment variables
ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1 \
    APPD_CONFIG_FILE=/app/controller_info.cfg

# Working directory
WORKDIR /app

# Copy requirements
COPY backend/requirements.txt .

# Install dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Copy backend code
COPY backend/ .

# Install AppDynamics Python Agent
COPY backend/appdynamics-pythonagent-25.x.x.x.tar.bz2 .
RUN pip install appdynamics-pythonagent-25.x.x.x.tar.bz2

# Copy AppDynamics config
COPY backend/controller_info.cfg /app/controller_info.cfg

# Expose Gunicorn port
EXPOSE 8000

# Optional static collection
RUN python manage.py collectstatic --noinput

# Start app with AppDynamics agent
CMD ["sh", "-c", "pyagent run -c /app/controller_info.cfg -- gunicorn -w 4 -b 0.0.0.0:8000 project.wsgi:application"]
```

---

## Build and Run the Container

### Build the Image

```bash
docker build -t pyagent-app .
```

### Run the Container

```bash
docker run -d \
  --name pyagent-container \
  -p 8000:8000 \
  pyagent-app
```

If your `controller_info.cfg` is outside the image, you can mount it instead:

```bash
docker run -d \
  --name pyagent-container \
  -p 8000:8000 \
  -v /path/to/controller_info.cfg:/app/controller_info.cfg \
  pyagent-app
```

---