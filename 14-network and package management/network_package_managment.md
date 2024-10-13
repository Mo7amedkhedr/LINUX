
## Networking in Linux

**Check Network Connectivity (ping Command)**

`$ ping <remote machine Address>` This command is used to check connectivity to the remote machine

•When you ping a destination,

1- A message ICMP_ECHO_REQUEST is sent to this destination

2- And a reply ICMP_ECHO_RESPONSE should be received from the remote destination

•This continues every N second period for a number of times, or until it is interrupted with a Ctrl-C

•Ping can also be used if you want to check the round trip delay to the destination

•You can specify destination by the IP address or by the Domain name

•If you have a network problem, check the following

•Ping the gateway to make sure it is accessible

•Ping the DNS Server

•Ping the destination by name and/or by address

**Tracing the Route (traceroute Command)**


`$ traceroute <destination Address>` Same as ping, but this time, you get the whole route of the packet

`$ traceroute www.google.com `Sometimes, certain nodes in the route remain hidden

**Collecting Network Statistics (netstat Command)**

`$ netstat [Options]` This command displays various network related information such as network connections, routing tables, interface statistics, etc.,

`$ netstat -r` To display the routing table information

To list network interfaces on the machine

`$ netstat -i` 

`$ netstat -ie (output similar to ifconfig)` 

To list statistics on sockets of different protocols

```
$ netstat -s
$ netstat -st (only for TCP Protocol)
$ netstat -su (only for UDP Protocol)
```

**Remote Access of a Machine (telnet Protocol)**

`$ telnet <destination Address>` The telnet is a protocol to enable the user at the client side to access a remote machine by opening a terminal on it

```
$ telnet 192.168.101.27
$ telnet bob@192.168.101.27
```


•The User will need to enter his login info

•A server application must be running on the destination machine to accept client connections

•Once connection is established, a `tty terminal` will be established on the remote machine that is controlled via the Telnet session

•Anything the user types is sent to the remote machine as if the user is using it


**Transporting files (ftp protocol)**

`$ ftp <Remote Machine Addrress>`

•This protocol enables the client to move files from/to the remote machine

```
$ ftp 192.168.101.12
$ ftp bob@192.168.101.12
```

•Sometimes an FTP server can allow anonymous login. In this case use,

```
Username: anonymous
Password: your email
```

* Once you login, you will be able to get/put files

```  
$ get myfile.txt
$ mget *.exe
$ put my_picture.png
$ mput *.jpg
```

•To exit  `$ bye`

**Secure login to remote machines (ssh protocol)**

`$ ssh <destination Address>`

•This is similar to the telnet protocol except for that the connection will be secured (traffic will be encrypted)

•To login securely to a machine,

```
$ ssh 192.168.101.100
$ ssh bob@ 192.168.101.100
$ ssh bob@tom-machine
```

•In the first time to connect to this machine, some confirmation will be requested to install the required keys for encryption

•Once connection is established, a `tty terminal` will be established on the remote machine that is controlled via the SSH session



**Secure File Copy (scp Command)**

```
$ scp <local filename> <user>@<remoteServer>:<remote-filename>
$ scp <user>@<remoteServer>:<remote-filename> <local filename>
```

•This command copies files from/to a remote machine

•It uses a secure channel similar to that of SSH

•Usage is similar to the ordinary copy command `cp` with the exception:

1- Remote filename is preceded by the remote server name, and optionally the user name

2- A username / password may need to be entered to complete the command

•The scp performs secure copy,

```
$ scp 192.168.101.13:my-doc.pdf ./my-docs/
$ scp bob@192.168.101.13:my-doc.pdf ./my-docs/
$ scp ./my-docs/*.pdf bob@remoteServer:.
$ scp -r ./documents bob@202.11.1.20:.
```

**Secure File Transfer (sftp Command)**

`$ sftp <remote Address>` This command has a similar usage as the normal ftp command

•However, it uses an SSH connection to secure the file transfer

```
$ sftp 192.168.1.103
$ sftp bob@192.168.1.103
```

•It has the same interface as ftp

•Note that sftp does not require an ftp daemon on the remote machine since it uses the ssh connection

**Downloading file from the Web (wget Command)**

`$ wget <URL of the file>`

•Very useful tool for downloading files from the web from the command line

`$ wget http://www.my-web-site.com/file.xml`

•Very useful in scripts that perform a download from the web













