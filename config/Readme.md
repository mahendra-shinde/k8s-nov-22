# Connect to Azure Kubernetes Service (AKS)

1. Download the cluster [credentials](https://raw.githubusercontent.com/mahendra-shinde/k8s-nov-22/main/config/credentials.yml) files 

1. Copy the file inside kube-config directory.

	```ini
	Location of kube-config:

	Windows :	C:\Users\USERNAME\.kube\
	Linux:      /home/USERNAME/.kube/
	MacOS:      /Users/USERNAME/.kube/
	```

1.	Rename your existing 'config' file and replace with new credentials.yml

	```powershell
	mv config config.old
	mv credentials.yml config
	```

1.	Test the connectivity using:

	```
	kubectl cluster-info
	kubectl get nodes
	```

## Kubectl : Kubernetes Client

* General Syntax for kubectl

	```
	kubectl [VERB] [ObjectType] [ObjectName] [OptionalSwitches]
	kubectl [OptionalSwitches] [VERB] [ObjectType] [ObjectName] 
	```

* kubectl examples

	```
	kubectl get nodes
	kubectl top nodes
	kubectl describe node aks-agentpool-57777951-vmss000000
	```

## Start with dedicated namespace

1.	Create namespace with YOURNAME 

	> Replace YOURNAME with actaul name in "lowercase"

	```
	kubectl create namespace YOURNAME
	```

1. 	Update current context and add namespace YOURNAME

	```
	kubectl config set-context --current --namespace=YOURNAME
	kubectl get pod
	```

1.	Get resources from "Other Namespace"

	```
	kubectl get po -n ANOTHER_NAMESPACE
	```
