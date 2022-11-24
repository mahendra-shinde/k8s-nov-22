# Kubernetes Probes

- Kubernetes has THREE types of probes:

	1. Startup Probe

		Delay the access to pod until it's ready !
		Once, probe returns SUCCESS, it wont repeat again.

	2. Liveness Probe

		Verify if POD is available / responding to probes.
		If NOT responding, restart the pod. (Recreating all containers !)
		It never stops !

	3.  Readiness Probe

		Verify if POD is available / responding to probes.
		It never stops !
		if NOT responding, the POD will be blacklisted, no request goes to this pod !

- Kubernetes has Three kinds of Probe Types

	1. HTTP Probe

		Test one URL and if it returns 4xx or 5xx then probe is failed.
		Test one URL and if it returns 2xx or 1xx (3xx) then probe is successful.

		Example

		```
		httpGet:
		  path: /
		  scheme: HTTP
		  port: 80
		```

	1. TCP probe

		Test by sending few packets of data, if returned, then SUCCESS or FAIL

		Example:
		```
		tcpProbe:
		  port: 3306
		```

	1. Command probe

		Run any Linux/Windows Shell command, if command returns an ERROR then FAIL.

		Example:

		```
		exec:
		  command:
		  - cat
		  - deployed.txt
		```

## Best practices:

1.	Use either TCP or Command probe as StartupProbe
2.  Use HttpProbe for Liveness and Readiness


## Demo

1.	Deploy the pod with 'livenessProbe'

	```
	kubectl apply -f 07-probe.yml
	kubectl get pod
	```

1.	Get inside the pod and delete index.html (Which results in Probe failure !)

	```
	kubectl exec -it pod-7 -- sh
	cd /usr/share/nginx/html
	rm index.html
	```

1.	Verify the pod status

	```
	kubectl get po -w
	## Press ctrl_c to stop !
	```

1.	Delete the pod-7 

	```
	kubectl delete po pod-7
	```

1.	Modify file `07-probe.yml` at line #11. Replace `livenessProbe` with `readinessProbe`

1.	Repeat the process for testing

	```
	kubectl apply -f 07-probe.yml
	kubectl exec -it pod-7 -- sh
	cd /usr/share/nginx/html
	rm index.html
	```

1.  Test the pod status

	```
	kubectl get pod -w
	## Press CTRL_C when you are tired !
	kubectl logs pod-7
	```