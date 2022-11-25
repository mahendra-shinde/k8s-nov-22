# Kubernetes Services

Kubernetes has THREE types of services:

1.	ClusterIP:		

		Default service type, which provides "Service IP" / VIP to set of pods (Managed by ReplicaSet or Deployment or StatefulSet)

		If you have either CoreDNS or KubeDNS installed in cluster, then
		Service will also have "DNS" name !


	Servic IP | Name | DNS   | FQDN
	----------|----|---|----
	10.2.123.12 | product-service | http://product-service/ | http://product-service.mahendra

		```yaml
		apiVersion: v1
		kind: Service
		metadata:
		  name: my-app
		spec:
		  selector:
		    app: app2
		    type: ClusterIP
		  ports:  
		  - targetPort: 80
		    port: 80
		```

## Cluster IP Service Demo

1.	Deploy the cluster-ip and deployment

	```
	kubectl apply -f 09-service-cluster-ip.yml
	kubectl get po,svc,deploy
	kubectl describe ep my-app	## List all endpoints (backend-pods)
	```

1.	Make one of the pod "Unavailable" by removing index.html

	```
	## Get name of FIRST pod using Powershell Variable
	$PODNAME=$(kubectl get po -l app=app2 -o=jsonpath="{ .items[0].metadata.name }")
	kubectl exec -it $PODNAME -- sh
	rm /usr/share/nginx/html/index.html
	exit
	```

1.	Wait for 1 Minute and then check all the endpoint of service `my-app`

	```bash
	kubectl describe ep my-app
	# Notice one pod in "NotReadyAddresses"
	```


1.	Remove failed pod

	```
	kubectl delete po $PODNAME
	```

1.	Test the clusterIp service:

	```
	$PODNAME=$(kubectl get po -l app=app2 -o=jsonpath="{ .items[0].metadata.name }")
	kubectl exec -it $PODNAME -- sh
	curl http://my-app
	curl http://my-app
	curl http://my-app
	exit
	```