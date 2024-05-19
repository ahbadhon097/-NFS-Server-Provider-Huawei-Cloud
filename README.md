# -NFS-Server-Provider-Huawei-Cloud
Setting up NFS server in a ubuntu virtual machine and the storage provides by Cloud Container Engine

Breakdown the Situation:

Limitation on Elastic Volume Service (EVS): As you are aware, Huawei Cloud Container Engine (CCE) EVS presently supports a maximum of one pod.

Scalable File Service Required: For multiple pods to access shared storage, a scalable file service like SFS is needed, but it's not included in the project.

Open Source NFS and CCE Integration: Setting up an open-source NFS server and utilizing a YAML file to integrate it with CCE is the suggested method.







 
