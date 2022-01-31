# external-storage-nfs-client - !NOT FOR PRODUCTION!

Based on a project: <https://github.com/kubernetes-sigs/nfs-subdir-external-provisioner>

For more details please
checkout: <https://examples.openshift.pub/cluster-configuration/storage/nfs/>  


### Deployment

#### Conntected

```bash
oc process -f https://raw.githubusercontent.com/openshift-examples/external-storage-nfs-client/main/openshift-template-nfs-client-provisioner.yaml \
  -p NFS_SERVER=192.168.51.1 \
  -p NFS_PATH=/srv/nfs-storage-pv-user-pvs  | oc apply -f -
```

#### Disconnected / air-gapped

##### Mirror image & artifactd

```bash
oc image mirror -a ${LOCAL_SECRET_JSON} \
  k8s.gcr.io/sig-storage/nfs-subdir-external-provisioner:v4.0.2 \
  ${LOCAL_REGISTRY}/${LOCAL_REPOSITORY}:nfs-client-provisioner-latest

curl -L -O https://raw.githubusercontent.com/openshift-examples/external-storage-nfs-client/main/openshift-template-nfs-client-provisioner.yaml
```

##### Deployment


```bash
oc process -f openshift-template-nfs-client-provisioner.yaml \
  -p NFS_SERVER=192.168.51.1 \
  -p NFS_PATH=/srv/nfs-storage-pv-user-pvs  \
  -p PROVISIONER_IMAGE=${LOCAL_REGISTRY}/${LOCAL_REPOSITORY}:nfs-client-provisioner-latest| oc apply -f -
```
