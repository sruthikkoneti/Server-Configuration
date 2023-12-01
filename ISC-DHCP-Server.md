# DHCP-Server

## Installation



```bash
apt-cache search dhcp | grep search isc-dhcp
```
Check if there is ```isc-dhcp-server```
```
sudo apt-get install isc-dhcp-server
```
The ISC-DHCP server is installed

## Configuration
```bash
cd /etc/dhcp
``` 
```bash
apt-get install isc-dhcp-server
```
1)List the directory to check if  `dhcpd.conf` is present or not\
2)Run this command to make a copy of the config file
```
sudo cp dhcpd.conf dhcpd.conf.bk 
```

Open the `dhcpd.conf` file now 
```bash
nano etc/dhcp/dhcpd.conf
```
At the end of the file, 
Add the following code:
```
# Config added by Sruthik 
#
subnet 10.102.142.0 netmask 255.255.255.0 {
option subnet-mask 255.255.255.0;
option broadcast-address 10.102.142.255;
option routers 10.102.142.1;


range 10.102.142.100 10.102.142.125;

}
``` 
where inplace of 10.102.142.0, place your `NETWORK ID` taken from IP address

After saving it,
```
sudo nano /etc/default/isc-dhcp-server
```
For 
```bash
INTERFACESv4=""
INTERFACESv6=""
```
add the interfce of your network by searching it in `ip a`

The code should look like
```bash
INTERFACESv4="wlo1"
INTERFACESv6=""
```

Now, test the DHCP server on another device which is in the same network, the device will get assigned a new IP address.
