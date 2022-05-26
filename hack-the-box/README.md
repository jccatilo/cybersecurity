# Hack-the-box guide. 
*date of creation: Quarter 1 of 2021*

***Requirements:***
1. Virtual Machine with Kali linux (or better, have a machine dedicated for Kali)
2. Installed OpenVPN on your Kali Machine.
3. VPN File from your hack-the-box account.

**Connecting to the VPN**
1. open your terminal and run your vpn using 
	```
	sudo openvpn <file_name>.ovpn
	```
	* *Wait for a confirmation message on your terminal indicating that the connection was successful.*
	* *insert screenshot here*
2. Press start on your machine of choice
	* *insert screenshot here*
3. To verify that the machine is up and your vpn connection is okay, ping the nachine you are connecting with in your Kali terminal.
	* *insert screenshot here*
4. If all goes well, you are all set.

**Scanning**
1. NMAP
	```nmap -A -p- -T4 X.X.X.X #IP address of the machine. ```
	- the goal is to look for open ports, know the services that are being run on the machine, know the versions and their vulnerablities that we can exploit.

# Under construction.