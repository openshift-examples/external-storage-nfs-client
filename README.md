# external-storage-nfs-client - !NOT FOR PRODUCTION!

Based on a project: <https://github.com/kubernetes-sigs/nfs-subdir-external-provisioner>

For more details please
checkout: <https://examples.openshift.pub/cluster-configuration/storage/nfs/>  


### Deployment
```bash
oc process -f https://raw.githubusercontent.com/openshift-examples/external-storage-nfs-client/main/openshift-template-nfs-client-provisioner.yaml \
  -p NFS_SERVER=192.168.51.1 \
  -p NFS_PATH=/srv/nfs-storage-pv-user-pvs  | oc apply -f -
```
