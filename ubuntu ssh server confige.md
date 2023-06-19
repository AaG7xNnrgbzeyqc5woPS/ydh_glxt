To configure an SSH server on Ubuntu, you can follow these steps:

### 1. Open the terminal with Ctrl+Alt+T and install the openssh-server package:
```
sudo apt update 
sudo apt install openssh-server
```
### 2. Once the installation is complete, the SSH service will start automatically. You can verify that SSH is running by typing:
```
systemctl status ssh
```
### 3. Ubuntu ships with a firewall configuration tool called UFW. If the firewall is enabled on your system, make sure to open the SSH port:
```
sudo ufw allow ssh
```
### 4. Finally, you can connect to your Ubuntu system using SSH by knowing the IP address of the computer and using the ssh command:
```
ssh username@address
```

Replace `username` with your actual user in the system and `address` with the IP address of your Ubuntu machine。


