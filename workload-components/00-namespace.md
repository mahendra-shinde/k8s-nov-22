# Kubernetes Namespace

1. Namespace is logical container for workload objects


1. Creating namespace using YAML manifest 

	```
	kubectl apply -f 00-namespace.yml
	kubectl get ns
	```

1.	Deleting the namespace

	```
	kubectl delete -f 00-namespace.yml
	```