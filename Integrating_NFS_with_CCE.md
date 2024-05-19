**Create a presistent volume**

**Prerequisite:**

* We've to make sure about the CCE cluster is actice in Huawei cloud console.
* And the require node has been pooled.


**Define a YAML file specifying the NFS server details and storage characteristics:**

`YAML`

```
apiVersion: v1
kind: PersistentVolume
metadata:
  name: nfs-pv
spec:
  capacity:
    storage: 10Gi
  accessModes:
    - ReadWriteMany
  nfs:
    server: <NFS_SERVER_IP>
    path: "/"
```

**Apply and use to create the PV.**

```
 kubectl apply -f nfs_pv.yaml
```

 **Create a Presistent Volume Claim (PVC):**

`YAML`

```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: nfs-pvc
spec:
  accessModes:
    - ReadWriteMany  #adjust access mode (ReadWriteOnce,ReadWriteMany)
  resources:
    requests:
      storage: 10Gi  #adjust requested size
storageClassName: " "    #leave empty if no storage class is used
```


**Apply and use to create the PVC :**

```
kubectl apply -f nfs_pvc.yaml
```

**Mount the volume in your pod Yaml: (optional)**

`YAML`

```
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
spec:
  containers:
    - name:my_container  
      image: nginx:latest   
      command: ["sleep","inf"]
  volumeMounts:
    -name: nfs-volume
     mountPath: /mnt/nfs
  volumes:
    -name: nfs-volume
  persistentVolumeClaim:  
     claimName: nfs-pvc
```

  
**Replace my-pod with your desired pod name and adjust container details if needed.

  Then select nodes for [configure NFS_Clienshare](https://github.com/ahbadhon097/-NFS-Server-Provider-Huawei-Cloud/blob/main/NFS_client_confuguration.md). 
