# Install AppDynamics .NET Core Agent on Windows Server 2019 (Docker & Local)

## Installation Steps

### 1. Download and Unzip
Download the .NET App agent package and unzip it to a temporary location.

### 2. Copy Agent Files
Copy all folders and `.dll` files into your application directory or a dedicated agent folder.

> **Note:** Make sure you have all the folders and dlls exactly as shown. Copy everything (including sub-folders) into your project's directory or the folder you'll be using for the deployment.

### 3. Set Environment Variables
The following variables must be set in your system or your container environment:

* `CORECLR_ENABLE_PROFILING` = `1`
* `CORECLR_PROFILER` = `{39AEABC1-56A5-405F-B8E7-C3668490DB4A}`
* `CORECLR_PROFILER_PATH_32` = `\AppDynamics.Profiler_x86.dll`
* `CORECLR_PROFILER_PATH_64` = `\AppDynamics.Profiler_x64.dll`

### 4. Configure AppDynamicsConfig.json
Update your `AppDynamicsConfig.json` with your Controller and Application details:

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

### 5. Application-Specific Config

Copy `AppDynamicsConfig.json` and rename it to `APPNAME.AppDynamicsConfig.json`.
*Replace `APPNAME` with your actual application `.exe` or `.dll` name.*

**Example:** `RazorPagesMovie.AppDynamicsConfig.json`

---

## Docker Integration

Inside your **Dockerfile**, ensure you include both the project files and the agent folder:

```dockerfile
FROM [mcr.microsoft.com/dotnet/aspnet:8.0](https://mcr.microsoft.com/dotnet/aspnet:8.0)

# Copy agent and project files
COPY appagent/ /opt/appdynamics/dotnet/
COPY RazorPagesMovie/ /opt/backend

WORKDIR /opt/backend

EXPOSE 8080

ENTRYPOINT ["dotnet", "RazorPagesMovie.dll"]

```

### Run the Container:

Use an environment file (`env`) to pass the variables during runtime:
`docker run -p 8080:8080 --env-file env test2`

---

## Troubleshoot

**Logs:** To check the logs, go to the path set in `AppDynamicsAgentLog.config`.

* **Default Path:** `C:\ProgramData\AppDynamics\DotNetAgent\Logs`

```

---