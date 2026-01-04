
# Installing and Configuring AppDynamics on Ubuntu Server

AppDynamics consists of three main components that must be installed separately:

1. **Controller & Enterprise Console** (The central management hub)
2. **Events Service** (Handles analytics and log data)
3. **EUM (End User Monitoring)** (Handles browser and mobile data)

---


2-Event Services:
-
1. Create Linux ( 16-32GB RAM, 1TB, 4 Cores)
2. Install Ubuntu
3. Open Ports 9080 :
   
   ```
   sudo ufw allow 9080/tcp
   sudo ufw reload
   ```
4. Set timedatectl
   ```
   sudo timedatectl set-timezone America/New_York
   ```

