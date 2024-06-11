**Create a presistent volume**

**Prerequisite:**

* We've to make sure about the CCE cluster is running in Huawei cloud console.
* And the required number of node has been pooled.
* Create Workloads and deployment using ubuntu image.
  

**Attaching required EVS to pv in CCE storage:**

`YAML`

```

kind: PersistentVolume
apiVersion: v1
metadata:
  name: pv-evs-nfs-test 
  uid: d4969c2f-c4ca-4dcd-8b38-990105a8d0ee
  resourceVersion: '4310'
  creationTimestamp: '2024-06-11T08:56:46Z'
  labels:
    failure-domain.beta.kubernetes.io/region: ap-southeast-3
    failure-domain.beta.kubernetes.io/zone: ap-southeast-3e
  annotations:
    everest.io/set-disk-metadata: 'true'
    pv.kubernetes.io/bound-by-controller: 'yes'
    pv.kubernetes.io/provisioned-by: everest-csi-provisioner
  finalizers:
    - kubernetes.io/pv-protection
    - everest.io/disk-metadata-protection
  managedFields:
    - manager: cfe-apiserver
      operation: Update
      apiVersion: v1
      time: '2024-06-11T08:56:46Z'
      fieldsType: FieldsV1
      fieldsV1:
        'f:metadata':
          'f:annotations':
            .: {}
            'f:pv.kubernetes.io/provisioned-by': {}
          'f:labels':
            .: {}
            'f:failure-domain.beta.kubernetes.io/region': {}
            'f:failure-domain.beta.kubernetes.io/zone': {}
        'f:spec':
          'f:accessModes': {}
          'f:capacity':
            .: {}
            'f:storage': {}
          'f:csi':
            .: {}
            'f:driver': {}
            'f:fsType': {}
            'f:volumeAttributes':
              .: {}
              'f:everest.io/disk-mode': {}
              'f:everest.io/disk-volume-type': {}
              'f:everest.io/enterprise-project-id': {}
              'f:storage.kubernetes.io/csiProvisionerIdentity': {}
            'f:volumeHandle': {}
          'f:persistentVolumeReclaimPolicy': {}
          'f:storageClassName': {}
          'f:volumeMode': {}
    - manager: everest-csi-controller
      operation: Update
      apiVersion: v1
      time: '2024-06-11T08:56:46Z'
      fieldsType: FieldsV1
      fieldsV1:
        'f:metadata':
          'f:annotations':
            'f:everest.io/set-disk-metadata': {}
          'f:finalizers':
            'v:"everest.io/disk-metadata-protection"': {}
    - manager: kube-controller-manager
      operation: Update
      apiVersion: v1
      time: '2024-06-11T08:57:03Z'
      fieldsType: FieldsV1
      fieldsV1:
        'f:metadata':
          'f:annotations':
            'f:pv.kubernetes.io/bound-by-controller': {}
        'f:spec':
          'f:claimRef':
            .: {}
            'f:apiVersion': {}
            'f:kind': {}
            'f:name': {}
            'f:namespace': {}
            'f:resourceVersion': {}
            'f:uid': {}
    - manager: kube-controller-manager
      operation: Update
      apiVersion: v1
      time: '2024-06-11T08:57:03Z'
      fieldsType: FieldsV1
      fieldsV1:
        'f:status':
          'f:phase': {}
      subresource: status
spec:
  capacity:
    storage: 10Gi
  csi:
    driver: disk.csi.everest.io
    volumeHandle: fae7c66e-ff0b-4a19-a56b-e5fe70a86217
    fsType: ext4
    volumeAttributes:
      everest.io/disk-mode: SCSI
      everest.io/disk-volume-type: GPSSD
      everest.io/enterprise-project-id: '0'
      storage.kubernetes.io/csiProvisionerIdentity: everest-csi-provisioner
  accessModes:
    - ReadWriteOnce
  claimRef:
    kind: PersistentVolumeClaim
    namespace: default
    name: test
    uid: 6e5fc847-9507-4807-b243-df47f66686c3
    apiVersion: v1
    resourceVersion: '4308'
  persistentVolumeReclaimPolicy: Retain
  storageClassName: csi-disk
  volumeMode: Filesystem
status:
  phase: Bound

```

**Attaching PV to PVC in CCE storage:**


`YAML`

```

kind: PersistentVolumeClaim
apiVersion: v1
metadata:
  name: test
  namespace: default
  uid: 6e5fc847-9507-4807-b243-df47f66686c3
  resourceVersion: '4325'
  creationTimestamp: '2024-06-11T08:57:03Z'
  labels:
    failure-domain.beta.kubernetes.io/region: ap-southeast-3
    failure-domain.beta.kubernetes.io/zone: ap-southeast-3e
  annotations:
    everest.io/disk-volume-type: GPSSD
    everest.io/enterprise-project-id: '0'
    pv.kubernetes.io/bind-completed: 'yes'
    volume.beta.kubernetes.io/storage-provisioner: everest-csi-provisioner
  finalizers:
    - kubernetes.io/pvc-protection
  managedFields:
    - manager: cfe-apiserver
      operation: Update
      apiVersion: v1
      time: '2024-06-11T08:57:03Z'
      fieldsType: FieldsV1
      fieldsV1:
        'f:metadata':
          'f:annotations':
            .: {}
            'f:everest.io/disk-volume-type': {}
            'f:everest.io/enterprise-project-id': {}
            'f:volume.beta.kubernetes.io/storage-provisioner': {}
          'f:labels':
            .: {}
            'f:failure-domain.beta.kubernetes.io/region': {}
            'f:failure-domain.beta.kubernetes.io/zone': {}
        'f:spec':
          'f:accessModes': {}
          'f:resources':
            'f:requests':
              .: {}
              'f:storage': {}
          'f:storageClassName': {}
          'f:volumeMode': {}
          'f:volumeName': {}
    - manager: kube-controller-manager
      operation: Update
      apiVersion: v1
      time: '2024-06-11T08:57:05Z'
      fieldsType: FieldsV1
      fieldsV1:
        'f:metadata':
          'f:annotations':
            'f:pv.kubernetes.io/bind-completed': {}
    - manager: kube-controller-manager
      operation: Update
      apiVersion: v1
      time: '2024-06-11T08:57:05Z'
      fieldsType: FieldsV1
      fieldsV1:
        'f:status':
          'f:accessModes': {}
          'f:capacity':
            .: {}
            'f:storage': {}
          'f:phase': {}
      subresource: status
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 10Gi
  volumeName: pv-evs-nfs-test
  storageClassName: csi-disk
  volumeMode: Filesystem
status:
  phase: Bound
  accessModes:
    - ReadWriteOnce
  capacity:
    storage: 10Gi

```


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
