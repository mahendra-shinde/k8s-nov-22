# ConfigMap

- Objects that stores Environment Variables / Configuration for pods
- Multiple Pods can share same configMap

## Demo

1.	Create the configmap and pod that uses config-map

	```
	kubectl apply -f 02-config-map.yml
	kubectl get pod
	kubectl get cm
	```

1.	Delete both configmap and pod

	```
	kubectl delete -f 02-config-map.yml
	```