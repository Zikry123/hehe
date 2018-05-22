<img width="108" alt="visualfieldlogo2" src="https://user-images.githubusercontent.com/39509760/40357347-78617d90-5dee-11e8-848f-c0fd4762203e.PNG">

&nbsp;

&nbsp;
&nbsp;
&nbsp;  
&nbsp;  


#  **Overview**

Smart cameras are able to track assets and people in order to maximise business revenues and reduce leakages by being "aware" of their surroundings.

### Features

- Tracks valuable assets to prevent any damages or misplacement.

- Tracks the number of customer footfall for each attraction.

- Ensure that the duration of the usage of assets adhere to the stipulated timing imposed to the customer.

- Immediate notice on which attraction require crowd control.

- Potentially alert lifesaving services in an event of a crisis.


### System requirements

- Ubuntu 18.04 LTS

- Nvidia Drivers

- CUDA Toolkit 9.1

- OpenCV 3.4.0
   gcc-<=6 and g++<=6, required for compiling CUDA within OpenCV (Ubuntu 18.04 LTS comes with gcc-7 and g++-7 as default)
  
- Darknet Yolo v3 (Specific version required) --> https://github.com/pjreddie/darknet/tree/yolov3  
   

-----------------------

#  **Animated Tutorial**

<div style="float:left; width:100%">
    <img src="https://raw.githubusercontent.com/facerecog/auto-ssh-tunnel/gh-pages/images/intro_video.gif" align="left" width=540px height=310px  /> 
</div>


&nbsp;
&nbsp;  
&nbsp;  
&nbsp;  
&nbsp;  
&nbsp;  
&nbsp;  
&nbsp;
&nbsp;  
&nbsp;  
&nbsp;  
&nbsp;  
&nbsp;  
&nbsp;  
&nbsp;  

-----------------------

# **Getting started** 



### Download

Clone the latest repository version from Github (recommended):  
`$ git clone https://github.com/facerecog/auto-ssh-tunnel.git`  

Alternatively, download the .tar.gz  file from the top of this page and unpack it:  
`$ wget https://github.com/facerecog/auto-ssh-tunnel/tarball/master  -O - | tar -xz `  


Now `cd` into the newly extracted directory.


### Installation 

__*Additional instructions for Mac OS X Users*__

  *Go to:  
System Preferences > Sharing. Turn on "Remote Login". Allow access for "All Users".*
&nbsp;  

1. Run  configuration.py  to specify the port, username, and IP address of the SSH server:  
`$ python configure.py <port> <username> <ip address>` 

2. Run the following command:  
`$ sudo python setup.py install`  

The installation will proceed automatically. If successful, the output of all the commands should roughly show:

```
Reading package lists... Done
Building dependency tree       
Reading state information... Done
openssh-server is already the newest version.
0 upgraded, 0 newly installed, 0 to remove and 118 not upgraded.
[*] Installing autossh client...
[*] Installing autossh as startup application...
mkdir: cannot create directory ‘.ssh’: File exists
yes: standard output: Broken pipe
yes: write error
Generating public/private rsa key pair.
Enter file in which to save the key (/root/.ssh/id_rsa): priv_key already exists.
Overwrite (y/n)? [*] Copying SSH-Keys file over to server...
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
"<username>@<ip address>" 's password: 
Number of key(s) added: 1

Now try logging into the machine, with:   "ssh ' "<username>@<ip address>" '"
and check to make sure that only the key(s) you wanted were added.

[*] Installing private keys inside protected folder...
yes: standard output: Broken pipe
yes: write error
[*] Moving autossh client into the /usr/local/bin/ directory...
[*] Moving private key to /etc/auto-ssh-tunnel/
mkdir: cannot create directory ‘/etc/auto-ssh-tunnel’: File exists
yes: standard output: Broken pipe
yes: write error

[*] We are now finished with the installation! Restart the client to complete the installation. To run autossh, input connect.py on the terminal.
```  
-------------------------


# **How the script works**  

During installation, the script will automatically append the following lines to /etc/ssh/ssh_config:
```
ServerAliveInterval 30
ServerAliveCountMax 4
```
It will also append the following to /etc/ssh/sshd_config
```
ClientAliveInterval 30
ClientAliveCountMax 4
```

Upon boot, the client will run `connect.py`, which sets up a reverse ssh tunnel. The server may now ssh into the client even if the client resides behind a NAT firewall.

-------------------------

# **Verify that it works**  

* From the client, ssh into your server:  
`$ ssh <rootname>@<ip address>`  

* Once in, connect back to your client:  
`$ ssh <your username>@localhost -p <port number specified as above>`

* If successful, you have just ssh-ed back into your client. Congratulations and enjoy!

-------------------------

# **Reverse SSH Tunnel Diagram**  

<img src="https://raw.githubusercontent.com/facerecog/auto-ssh-tunnel/gh-pages/images/Client-server%20diagram.png"/>


-------------------------

# **Uninstall**  

To uninstall:
`$ sudo rm -rf /etc/init.d/connect.py /etc/auto-ssh-tunnel /usr/local/bin/connect.py /System/Library/StartupItems/auto-ssh-tunnel/`  


-------------------------

# **Support**  

If you want to support this project, please consider reaching out to me via  muhd.amrullah@facerecog.asia  


-------------------------  
Property of Facerecog Asia Pte. Ltd. and 26 Factorial
