Here’s a refined version of your Python agent guide that keeps the **authentic, hands-on feel**, but improves clarity, structure, and consistency without over-polishing it.

---

# Installing the AppDynamics Python Agent

## Prerequisites

* Python application
* (Optional but recommended) Virtual environment
* Access to the AppDynamics Controller (host, port, account, access key)

---

## Installation Steps

### 1. Navigate to the Application Directory

Change to the directory where your Python application resides:

```bash
cd /path/to/your/application
```

---

### 2. Activate the Virtual Environment (If Present)

If your application uses a virtual environment, activate it:

```bash
source env/bin/activate
```

---

### 3. Install the AppDynamics Python Agent

You can install the agent using **pip**:

```bash
pip install appdynamics
```

Alternatively, if you have the agent package as a tarball:

1. Extract the package:

```bash
tar -xjf appdynamics-pythonagent-25.x.x.tar.bz2
```

2. Install the wheel file:

```bash
pip install appdynamics-pythonagent-xxx.whl
```

---

### 4. Create the Controller Configuration File

Create a configuration file named `controller_info.cfg`.

Example configuration:

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

Ensure the values match your AppDynamics Controller details.

---

### 5. Start the Application Using the Python Agent

Run your Python application through the AppDynamics agent wrapper.

Example using **Gunicorn**:

```bash
pyagent run -c path_to/controller_info.cfg -- gunicorn -w 4 -b 0.0.0.0:8000 project.wsgi:application
```

This starts the server with the AppDynamics Python agent enabled and reporting metrics to the controller.

---