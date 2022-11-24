# Kubernetes Manifests

Kubernetes use "Declarative Approach" for workload components.

The Workload object is "described" in a YAML file.

> extension used by manifest is YAML or YML

> kubectl doesn't need extension for manifest files

All these YAML files are called "Manifests" and each object type has its own "Schema"

The official API Reference guide is available [here](https://v1-24.docs.kubernetes.io/docs/reference/generated/kubernetes-api/v1.24/).

## kubectl commands for YAML manifests

1.	Creating new workload object using YAML manifest.

	Limitation: Fails if object exists !

	`kubectl create -f <filename> or <url>`

1.	Create or Upate workload oject using YAML manifest.

	`kubectl apply -f <filename> or <url>`

1.	Delete the workload object(s)

	`kubectl delete -f <filename> or <url>`
