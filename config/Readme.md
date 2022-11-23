# Connect to Azure Kubernetes Service (AKS)

1. Download the cluster credentials files 
	`https://raw.githubusercontent.com/mahendra-shinde/k8s-nov-22/main/config/credentials.yml`

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
