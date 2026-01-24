# Install AppDynamics .NET Core Agent on Windows Server 2019

## Installation Steps

### 1. Download and Unzip
Download the .NET App agent package and unzip it to a temporary location.

### 2. Copy Agent Files to Project
Copy and paste **all files and folders** (including all `.dll` files) into your application directory.

> **Important:** Make sure you have all the folders and dlls exactly as shown in the package. Copy everything into your project’s root directory to ensure the profiler can find the necessary dependencies.

### 3. Set Environment Variables
You must set the following environment variables in your system to enable the .NET Core profiler:

* `CORECLR_ENABLE_PROFILING` = `1`
* `CORECLR_PROFILER` = `{39AEABC1-56A5-405F-B8E7-C3668490DB4A}`
* `CORECLR_PROFILER_PATH_32` = `\AppDynamics.Profiler_x86.dll`
* `CORECLR_PROFILER_PATH_64` = `\AppDynamics.Profiler_x64.dll`

### 4. Configure AppDynamicsConfig.json
Locate the `AppDynamicsConfig.json` file and update the controller and application details:

```json
{
  "controller": {
    "host": "192.168.1.121",
    "port": 8090,
    "account": "customer1",
    "password": "your-access-key"
  },
  "application": {
    "name": "RazorPagesMovie",
    "tier": "tier1",
    "node": "node1"
  }
}

```

### 5. Create Application-Specific Config

Copy `AppDynamicsConfig.json` and rename it to `APPNAME.AppDynamicsConfig.json`.
*Replace `APPNAME` with your actual application `.exe` or `.dll` name.*

**Example for RazorPagesMovie:**
File name: `RazorPagesMovie.AppDynamicsConfig.json`

```json
{
  "controller": {
    "host": "192.168.1.121",
    "port": 8090,
    "account": "customer1",
    "password": "3dc71574-62fd-48ac-bdea-20dc6cc70b9e"
  },
  "application": {
    "name": "RazorPagesMovie"
  }
}

```

---

## Troubleshoot

If the agent is not reporting to the controller, check the logs.

* **Log Path:** Refer to the path set in `AppDynamicsAgentLog.config`.
* **Default Location:** `C:\ProgramData\AppDynamics\DotNetAgent\Logs`

```

---