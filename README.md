# homelab-charts

## Installation

Add the repo:

```
helm repo add homelab-charts https://bpmb82.github.io/homelab-charts
```

Install a chart (e.g. sonarr):

```
helm install sonarr homelab-charts/sonarr --values=values.yml
```

## Custom values

Please make sure you define a PV and PVC for the 'config' and 'downloads' folders. A single 'downloads' folder is used for all applications so they can move files instead of having to copy them.

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
