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
