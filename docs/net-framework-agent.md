# How to Install App Agent for .NET Framework 4.8 using IIS

## Prerequisites
* **IIS Check:** Ensure your application is running inside Windows IIS.
* **Enable IIS:** If IIS is not enabled, you can enable it via **Windows Features**.

## Installation Steps

### 1. Prepare Installer
Copy the **.NET App Agent MSI Installer** onto your machine.

### 2. Run the Wizard
Run the MSI installer and follow the installation wizard steps.

### 3. Controller Configuration
When the installer asks for the Controller details, provide:
* **Controller Host:** (IP Address or Hostname)
* **Port:** (Default is usually 8090)
* **Access Key:** (Your Controller account key)

### 4. Test Connectivity
Click the **"Test Connection"** button to verify the agent can communicate with the controller before proceeding.

### 5. Tier and Node Setup
Choose the option to **"Automatically configure tier and nodes"** for a standard setup.

### 6. Restart & Load Generation
Restart your application to initialize the agent.
> **Note:** You can perform the restart directly within **IIS Web Applications**.

Generate load on your app by clicking through the pages to trigger data reporting.

### 7. Final Verification
Check the **App Agent panel** in the Controller UI to confirm the nodes are appearing.

---

## Troubleshoot

If you don't see data, check the .NET agent logs at the following path:
* **Log Location:** `%programdata%/appdynamics/DotNetAgent/Logs/AgentLog*.txt`

```

---