<b>Create a presistent volume<b>


Prerequisite:

1. We've to make sure about the CCE cluster is actice in Huawei cloud console.
  
2.And the require node has been pooled.


Define a YAML file specifying the NFS server details and storage characteristics:

`YAML`
  
`apiVersion: v1`
kind: PersistentVolume
metadata:
  name: nfs-pv
spec:
  capacity:
    storage: 10Gi  # Adjust storage size as needed
  accessModes:
  - ReadWriteOnce  # Adjust access mode (ReadWriteOnce, ReadWriteMany)
  nfs:
    server: <NFS_SERVER_IP_OR_HOSTNAME>  # Replace with your NFS server IP/hostname
    path: /<exported_directory_path>  # Replace with the NFS share path
  persistentVolumeReclaimPolicy: Recycle`
