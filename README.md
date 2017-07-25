# openshift-persistentvolume
Actual documentation: https://docs.openshift.org/latest/architecture/additional_concepts/storage.html  
1. Create a PV for the namespace:
```
oc create -f pv.yml -n <namespace>
```  

2. Make a claim to the PV:  
```
oc create -f pvc.yml -n <namespace>
```  

3. Pod volume claim:  
```
oc create -f pod.yml -n <namespace>
```


# NFS Export
1. Both NFS and client must be in same domain. In /etc/idmapd.conf:  
```
domain = localdomain.com
```  
2. Disable idmap:
```
echo 'Y' > /sys/module/nfsd/parameters/nfs4_disable_idmapping
```  
3. The export:
```
/openshift *(rw,sync,root_squash)
```  

Original doc:  
https://bugzilla.redhat.com/show_bug.cgi?id=1402257  
https://docs.openshift.org/latest/install_config/persistent_storage/persistent_storage_nfs.html#nfs-additional-config-and-troubleshooting  


