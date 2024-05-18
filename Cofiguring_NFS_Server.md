Installing NFS server in a Ubuntu VM 

<b>Update Package Lists:<b>
Ensure you have the latest package lists: 
`sudo apt update` 

<b>Install NFS Server Package:<b>
Install the nfs-kernel-server package to enable NFS server functionality:
`sudo apt install nfs-kernel-server`

<b>Make a directory to create the path<b>
`sudo mkdir -p /mnt/nfs_share`







