# Kubernetes ReplicaSets

- Provides Manual and Auto-Scaling (Using HPA) for Pods
- Logical group of Pods (All the pods share same config/template)
- Manually scale using command :

	`kubectl scale rs <rs-name> --replicas=N`

	Where:
		Minimum value of N is Zero !!

## Demo

- Deploy and test ReplicaSet

	```
	kubectl apply -f 05-replica-set.yml
	kubectl get po -l app=app1
	kubectl get rs
	kubectl delete po -l app=app1
	kubectl get po -l app=app1
	```

- To watch the pods getting created and terminated, use comand:

	```
	kubectl get po -l app=app1 -w
	```

- To "Manually Scale"

   ```
   kubectl scale rs/set1 --replicas=3
   kubectl get po -l app=app1
   kubectl scale rs/set1 --replicas=0
   ```