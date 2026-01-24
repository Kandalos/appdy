# Installing the AppDynamics App Agent for a Windows Service  
**Windows Server 2019**

## Prerequisites
- Windows Server 2019
- A .NET–based Windows Service application
- AppDynamics Controller access (host, port, access key)

---

## Installation Steps

### 1. Verify the Application Is a .NET Application
Ensure the target Windows service is running on the .NET framework.

Run the following command from an elevated Command Prompt:
```cmd
tasklist /m "mscor*"
```

If the service appears in the output, it is a .NET application.

---

### 2. Install the .NET App Agent
Install the AppDynamics .NET App Agent on the server where the Windows service is running.

---

### 3. Open the Agent Configuration Utility
After installation, launch the **Agent Configuration Utility** from the AppDynamics installation directory.

---

### 4. Select Manual Installation
When prompted for the installation type, choose **Manual Installation**.

---

### 5. Complete Basic Configuration
Provide the following details:
- Controller host
- Controller port
- Access key

Once completed, finish the installation.

---

### 6. Configure the Agent Configuration File
Edit the `config.xml` file located at:

```
C:\ProgramData\AppDynamics\Config\
```

Below is an example configuration:

```xml
<?xml version="1.0" encoding="utf-8"?>
<appdynamics-agent xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">

  <controller host="192.168.1.121" port="8090" ssl="false" enable_tls12="false">
    <application name="MyService" />
    <account name="customer1"
             password="3dc71574-62fd-48ac-bdea-20dc6cc70b9e" />
  </controller>

  <machine-agent />

  <app-agents>
    <IIS>
      <automatic enabled="false" />
    </IIS>

    <standalone-applications>
      <standalone-application executable="C:\MyService\runner.bat"
                              command-line="-x">
        <tier name="Windows Service Tier" />
      </standalone-application>
    </standalone-applications>
  </app-agents>

</appdynamics-agent>
```

---

### 7. Restart the Windows Service
Restart the Windows service to ensure the AppDynamics agent is loaded and begins reporting data to the controller.

---