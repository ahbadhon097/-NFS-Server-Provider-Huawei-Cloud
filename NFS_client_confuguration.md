**Installing NFS Client server**

**Update Package Lists:**


```
 sudo apt update
```

---

**Install NFS Client Server Package:**

Install the nfs-common package to enable NFS client server functionality:

```
sudo apt install nfs-common
```

---

Then make a directory for creating a path for clientshare.

```
sudo mkdir -p /mnt/nfs_clientshare
```

---

<b>Then mount the nfs_share<b>

```
sudo mount <nfs_server_ip>:/mnt/nfs-share /mnt/nfs_clientshare
```

The directory /mnt/nfs-share on the NFS server with IP <nfs_server_ip> is mounted onto the local directory /mnt/nfs_clientshare on your system.

---
