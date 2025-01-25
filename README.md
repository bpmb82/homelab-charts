# homelab-charts

## Custom values

Please make sure you define a PV and PVC for the 'config' and 'downloads' folders.

### Example PV
```
---
apiVersion: v1
kind: PersistentVolume
metadata:
  name: "config"
  labels:
    type: "local"
spec:
  storageClassName: "config"
  capacity:
    storage: "200Gi"
  accessModes:
    - ReadWriteMany
  hostPath:
    path: "/mnt/ssd/media"
---
```

### Example PVC
```
---
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  namespace: "sonarr"
  name: "config"
spec:
  storageClassName: "config"
  accessModes:
    - ReadWriteMany
  resources:
    requests:
      storage: "200Gi"
---
```
