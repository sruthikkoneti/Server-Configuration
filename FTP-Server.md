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
Configure the ownership of the user
```bash
sudo chown nobody:nogroup /home/$(user1)/ftp
```
```bash
sudo chmod a-w /home/$(user1)/ftp
```
Create a directory for user to access for transfers
`dir_name`=`uploads`
```bash
sudo mkdir /home/$(user1)/ftp/dir_name
```
```bash
sudo chown $(user1):$(user1) /home/$(user1)/ftp/dir_name
```
```bash
echo "my FTP server" | sudo tee /home/$(user1)/ftp/dir_name/demo.txt
```
You can check the persmission for ftp directory by running this command
```bash
sudo ls -la /home/$(user1)/ftp
```
Add the created user to FTP users list to login
```bash
echo "some-text" | sudo tee -a /etc/vsftpd.userlist
```
Restart FTP server to apply the changes
```bash
sudo systemctl restart vsftpd
```
Open the config file again and slide to the bottom
```bash
sudo nano /etc/vsftpd.conf
```
Add the piece of code so that the server only allows access users who are in the local database
``bash
userlist_enable=YES
userlist_file=/etc/vsftpd.userlist
userlist_deny=NO
```
