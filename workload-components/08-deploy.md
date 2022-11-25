# Deployment represents a single application or component in distributed application.

- Deployment Objects offers maintaining revision history (deployment history)
- Easy "Rollback" to previous version
- Contains multiple ReplicaSets, of which only ONE replica-set would be ACTIVE
- Deployment history is actually just group of ReplicaSets with "Replica count" set to ZERO.

## Rollout commands:

```bash
kubectl rollout status deploy/app1				## app1 is deployment name
kubectl rollout undo deploy/app1				## Switch to LAST version
kubectl rollout undo deploy/app1 --to-revision=2 ## Switch to revision number 2
kubectl rollout history deploy/app1				## All Revisions / versions
kubectl rollout pause deploy/app1				## DO NOT DISTURB mode 
kubectl rollout resume deploy/app1				## 
```

## Demo

```
kubectl apply -f 08-deploy1.yml
kubectl get rs,deploy 	## No space before and after ","
kubectl set image deploy/app1 myapp=mahendrshinde/myweb:2 --record
kubectl get rs,pod
kubectl set image deploy/app1 myapp=mahendrshinde/myweb:3 --record
kubectl get rs,pod
kubectl rollout history deploy/app1
kubectl port-forward deploy/app1 8080:80
## New Shell/Terminal
curl http://localhost:8080/
## Go back to old terminal and press CTRL_C to stop port-forwarding
kubectl rollout undo deploy/app1
kubectl get rs,pod
kubectl port-forward deploy/app1 8080:80
## New Shell/Terminal
curl http://localhost:8080/
kubectl delete -f 08-deploy1.yml
```

## Update Strategy

- Deployment object has TWO update strategies:

1. recreate [Default]

	Terminate ALL the pods of OLD replicaset and Then create pods in NEW replicaset.
	Minimal downtime observed.

2.	rollingUpdate

	Terminate OLD pods in batches (default batch size : 1) and deploy NEW pods as well.
	Repeat the process till OLR replicaSet is set to ZERO.

	```yml
	  strategy:
	    rollingUpdate:
	    maxSurge: 1       ## Temp Scale UP by 1 Instance ## replicas would be 3
	    maxUnavailable: 2 ## Take TWO pods down each time ! / Default is 1
	```




> Official Docs : https://kubernetes.io/docs/concepts/workloads/controllers/deployment/