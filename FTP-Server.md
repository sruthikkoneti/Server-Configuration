# FTP Server

## Installation



```bash
sudo apt install vsftpd
```
Check the status of FTP Server using the below command
```
sudo service vsftpd status
```
You can see FTP is active and running smoothly

## Configuration
```bash
cd /etc
``` 
1)List the directory to check if  `vsftpd.conf` is present or not\

Open the `vsftpd.conf` file now 
```bash
sudo nano etc/vsftpd.conf
```
Uncomment this to allow local users to log in.
`local_enable=YES`

Uncomment this to enable any form of FTP write command.
`write_enable=YES`

At the end of the file, 
Add the following code:
```bash
user_sub_token=$USER
local_root=/home/$USER/ftp
passv_min_port=10000
passv_max_port=10100
``` 
Now save it by pressing `Ctrl+X` and then `Y`

Configure the Firewall and open the ports
```bash
sudo ufw allow from any to any port 20,21,10000:10100 proto tcp
```
Now, the ports are open and ready to accept the traffic

Create a user who can access FTP on the device
```bash
sudo adduser $(user1)
```
Create an FTP folder for the user in the home directory
```bash
sudo mkdir /home/$(user1)/ftp
```
