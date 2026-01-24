# Install AppDynamics .NET Core Agent on LINUX

## Installation Steps

### 1. Download and Unzip
Download the .NET App agent for Linux and unzip the package to your preferred directory.

### 2. Copy Agent Files
Copy all folders and `.dll` files into your application folder or a dedicated agent directory.
> **Note:** Make sure you have all the folders and dlls exactly as shown in the package. Copy everything (including sub-folders).

### 3. Set Environment Variables
You need to set these variables for the profiler to attach to your .NET process.
**Tip:** On Ubuntu Linux, you can set these globally in `/etc/environment`.

* `CORECLR_ENABLE_PROFILING` = `1`
* `CORECLR_PROFILER` = `{57e1aa68-2229-41aa-9931-a6e93bbc64d8}`
* `CORECLR_PROFILER_PATH` = `<full_path_to_profiler_folder>/libappdprofiler.so`

### 4. Configure AppDynamicsConfig.json
Update the `AppDynamicsConfig.json` with your Controller details:

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
*Replace `APPNAME` with your actual application executable or .dll name.*

**Example:**
If your app is `RazorPagesMovie`, run it with:
`./RazorPagesMovie`

---

## Troubleshoot

> **Important Note:** Currently, there are limited known ways to view internal agent logs for .NET Core on Linux.

**If the agent is not reporting:**

1. **Verification:** Double-check that all files and config JSONs are in the correct directory as shown above.
2. **Connectivity:** Check your connection to the controller host (ensure port 8090 is open).
3. **Environment:** Run `printenv` to ensure the `CORECLR` variables are actually loaded in your session.

```

---