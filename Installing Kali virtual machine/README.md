How to use hack the box

prerequisites:
1.) install openvpn 
2.) download your acounts vpn file

Capturing flags:
1.) open your terminal and run your vpn using "sudo openvpn vpn_file.ovpn"
2.) Press start on your machine
3.) To verify that the machine is up and your vpn connection is okay, ping the machine in your terminal
4.) you are all set.

Scanning
1.) NMAP
	nmap -A -p- -T4 X.X.X.X #IP address of the machine. 
	>the goal is to look for open ports, know the services that are being run on the machine, know the versions and their vulnerablities that we can exploit.

