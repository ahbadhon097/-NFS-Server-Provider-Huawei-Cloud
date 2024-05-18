Installing NFS server in a Ubuntu VM 

Update Package Lists:

Ensure you have the latest package lists: 

`sudo apt update` 

--------------------

Install NFS Server Package:

Install the nfs-kernel-server package to enable NFS server functionality:

`sudo apt install nfs-kernel-server`

--------------------

You may use the following command at a terminal prompt to launch the NFS server

`sudo systemctl start nfs-kernel-server.service`

--------------------
Make a directory to create the path

`sudo mkdir -p /mnt/nfs_share`

--------------------
Change the ownership for new group and new user for the directory `/mnt/nfs_share`

`sudo chmod 777 /mnt/nfs_share`

--------------------

Then launch editor to  edit `/etc/exports` file for modifying the system configuration 

On your ubuntu system, the NFS server is configured via the `/etc/exports` file. It details the directories you wish to share and the permissions for other devices on the network to access those directories.

`sudo vim /etc/exports`

--------------------
After executing editor , we've to give the path of the directory where we want to get the access to read/write and sync the nfs server.You can configure the directories to be exported by adding them to the /etc/exports file. For example:

`mnt/nfs_share <your NFS_server_ip>(rw,sync,no_subtree)`

--------------------


 Apply the new config via:

`sudo exportfs -a`

--------------------

Now, You may use the following command at a terminal prompt to restart the NFS server

`sudo systemctl restart nfs-kernel-server`

--------------------

then the below command, sudo ufw allow from the dedicated to any port nfs, is used on a Linux system with the firewall tool ufw to configure firewall rules for allowing access to an NFS server. The ip defines the source of the allowed traffic. In this case, it's restricting access to traffic originating from the IP address. You can replace this with a specific IP address or a subnet if you want to allow access from multiple machines.If we use the multiple nodes from CCE clusters as a client then we have to allow those nodes ip which are used to store the data as a `NFS_CLIENT` .

`sudo ufw allow from 192.143.12.4 to any port nfs`

--------------------
Important Consideration:

Crucial Points to Remember:

Specificity: Although this command permits access from a single IP, if you need to permit access froTo start the NFS server, you can run the following command at a terminal prompt:m several computers, you might want to use a subnet or firewall groups.
Security: It may not always be the best idea to provide access from any port using any. It is advised to specifically identify the ports your NFS server is utilizing if you are aware of them in order to improve security.Crucial Points to Remember:

Specificity: Although this command permits access from a single IP, if you need to permit access from several computers, you might want to use a subnet or firewall groups.
Security: It may not always be the best idea to provide access from any port using any. It is advised to specifically mention the ports your NFS server is utilizing if you are aware of them for.

Configuring the NFS Server: Keep in mind that this operation simply sets up the firewall. Additionally, you must set up the NFS server itself using tools like rpc.mountd or the configuration settings in your NFS server software to permit access from the designated IP address or subnet.

--------------------
Enable the uncomplicate firewall :

Once we start the activity of the firewall we've to remember that the SSH connection could be interrupt.So before leaving the virtual machine or local server we need to disable the firewall.

`sudo ufw enable `

--
for disable the firewall 

`sudo ufw disable `



--------------------
Now we can check the status of the firewall

`sudo ufw status `






















