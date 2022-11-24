# Pod

- Smallest Unit in workload types
- Pod is collection of "Containers" which are deployed as "Single Unit"
- Every POD is assign a private IP address. (Referred as "Pod-IP")
- All containers inside the pod share same Pod-IP address.

## Multi Container Pod Use Cases
1. 	SideCar Containers

	- One Application container
	- Additional Containers for monitoring, logging or authentication/authorization.
	- All containers will be always running

1.	InitContainer
	- One Application container
	- Additional "Init" containers who is "responsible" to initialize "Main Container"
	- Unless Init container has "DONE" its task, entire POD will remain "Unavailable"
	- InitContainer is "Deleted" after task is completed.

1.	Creating Pod using YAML Manifest

	```
	kubectl apply -f 01-pod.yml
	kubectl get pod
	kubectl get pod -l app=myapp1
	kubectl delete pod -l app=myapp1,version=1.1.2
	```