1. create a PV pv001.yaml
```
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv001
  namespace: openshift
spec:
  accessModes:
  - ReadWriteOnce
  capacity:
    storage: 5Gi
  hostPath:
    path: /registry
  persistentVolumeReclaimPolicy: Retain
  claimRef:
    apiVersion: v1
    kind: PersistentVolumeClaim
    namespace: default
    name: pv01-ref 
```
2. Create the PV.
```
oc create -f pv001.yaml
```

3. Verify that PV has claim name and Avaiable.
```
# oc get pv pv001 
NAME      CAPACITY   ACCESSMODES   RECLAIMPOLICY   STATUS    CLAIM              REASON    AGE
pv001     5Gi        RWO           Recycle         Available     default/pv01-ref             5m
```

4. Create PVC pvc-01.yaml
```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: pv01-ref
  namespace: default
spec:
  accessModes:
  - ReadWriteOnce
  resources:
    requests:
      storage: 5Gi
```

5. Create PVC in OCP.
```
oc create -f pvc-01.yaml
```

6. The PV status will changed from Available to Bound.
```
#oc get pv pv001 
NAME      CAPACITY   ACCESSMODES   RECLAIMPOLICY   STATUS    CLAIM              REASON    AGE
pv001     5Gi        RWO           Recycle         Bound     default/pv01-ref             5m
```

