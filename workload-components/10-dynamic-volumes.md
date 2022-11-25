# Dynamic Volumes

- Kubernetes uses "Dynamic Volume provisioning" for creating and linking external storage to volume.
- Cluster must have "Storage Provisioner" installed for each storage service type.
- Each "Storage Provisioner" may support one or more "Storage Classes"
- You can create "Formal Request" for allocating new volume using "PersistentVolumeClaim" (PVC)
	
	PVC with "Immediate" binding would create "PersistentVolume" (PV) as soon as claim is created !
	
	PVC with "WaitForFirstCosumer" binding would create "PV" only when "FIRST POD" that uses PVC is deployed.

What should happen to "Actual Storage backend" when PV is deleted?

## Reclaim Policy:

- Delete:

	You delete PV, the actual storage is deleted as well (Total Data LOSS).

- Recycle:

	You delete PV, the actual storage is FORMATTED / CLEANED (Total Data LOSS).

- Retain:

	You delete PV, the actual storage is DETACHED from cluster and data is retained.


## Demo : PVC

```
kubectl apply -f 10-claim1.yml
kubectl get pvc,pv 
kubectl delete -f 10-claim1.yml
kubectl get pvc,pv 
```