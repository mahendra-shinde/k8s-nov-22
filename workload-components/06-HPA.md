# HorizontalPodAutoScaler (HPA)

- Performs "auto-scaling" of ReplicaSet or Deployment or StateFulSet.
- Only responsible for "Calculating" number of instances required for application.
- Once calculation is done, it will update/notify the replicaset controller.

## Pre-requisites:

1.	HPA depends on `Metrics Server` extension installed in cluster.

	```
	kubectl top nodes
	kubectl top pods
	```

1. Every Pod (Container) should have "resource request" defined.

## Calculation

`desiredReplicas = ceil[currentReplicas * ( currentMetricValue / desiredMetricValue )]`

## Scenario 1

1. 	Pod has following resource request:

	```yaml
	resources:
	  requests:
	    cpu: 100m
	```

1.	Pods actual CPU Usage is `80m` which is `80%` Current instance is 1

1.	HPA has following target:

	```yaml
	  targetCPUUtilizationPercentage: 50
	```

	desiredReplicas = ceil [ 1 * (80/50) ] = 2

## Scenario 2

1. 	Pod has following resource request:

	```yaml
	resources:
	  requests:
	    cpu: 100m
	```

1.	Pods actual CPU Usage is `20m` which is `20%` Current instance is 2

1.	HPA has following target:

	```yaml
	  targetCPUUtilizationPercentage: 50
	```

	desiredReplicas = ceil [ 2 * (20/50) ] = 1

## HPA v1 Demo

```
kubectl apply -f 06-HPA.yml
kubectl get pods
# Wait for 1 minute
kubectl get hpa
kubectl describe hpa
kubectl delete -f 06-HPA.yml
```

## HOA v2 Demo