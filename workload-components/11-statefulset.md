# Stateful Set

- Alternative to deployment object
- Supports auto-scaling, manual scaling & rollout
- Ordered Creation/Deletion of Pods 

	Pod with Highest INDEX value will be deleted first
	
	New Pod will be last-index+1

- Every pod gets an identity (which is <SETNAME>-<INDEX>)
- Pods use PersistentVolumeClaimTemplate, creates new PVC claim per pod.

## Demo

```
kubectl apply -f 11-statefulset.yml
kubectl get pod,sts

kubectl scale sts/app4 --replicas=4
kubectl get pod -l app=app4 -w
```

### How to STS

```
kubectl scale sts/app4 --replicas=0
kubectl delete sts/app4
kubectl delete pvc www-app4-0 
kubectl delete pvc www-app4-1
kubectl delete pvc www-app4-2
kubectl delete pvc www-app4-3
```