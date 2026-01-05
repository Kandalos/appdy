Event Services:
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
5. Create The SSH Key
   On Enterprise Console Server do:
   ```
   mkdir -p ~/.ssh
   chmod 700 ~/.ssh
   cd ~/.ssh
   ssh-keygen -t rsa -b 2048 -v -m pem -f appd-ssh
   ```
   then copy the publickey into your events service host:
   ```
   scp ~/.ssh/appd-ssh.pub user@host:~/
   ```
6. Create ```/opt/appdynamics``` :
   Create the directory and give the current user ownership:
   ```
   mkdir /opt/appdynamics
   chown -R appdy:appdy /opt/appdynamics
   ```
7. Add the host in Enterprise Console
   for ssh private key you need the key in controller host:
   ```
   cat ~/.ssh/appd-ssh
   ```
8. Install the Events Services using the installer in enterprise console
   
   
