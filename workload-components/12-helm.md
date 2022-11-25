# Helm [ Package Manager for Kubernetes ]

- Single Executable.
- Access to 100s of public Helm repositories.
- Works with All kubernetes clusters (On-premise, Cloud Managed, Dev/Test )
- Easy installation of packages and extensions for kubernetes


# Central Registry or Search engine for Helm Packages 

Use https://artifacthub.io as search engine for public repositories.


## Demo : Installing Kubernetes dashboard (Web UI) using Helm

1.	Download the Helm executable from  .
1.	Extract "Helm.exe" to c:\helm folder (Create folder first !)
1.	Edit "Environment Variable PATH" of windows-os to include "C:\helm" folder.
1.  Open new powershell and install the repository and update it.

	```
	helm repo add kubernetes-dashboard https://kubernetes.github.io/dashboard/
	helm repo update
	```

1.	Install dashboard in new namespace

	```
	kubectl create namespace web-ui
	helm install web-ui -n web-ui kubernetes-dashboard/kubernetes-dashboard
	```

1.	Find the POD and forward the port 8443 to localhost

	```
	$POD_NAME=$(kubectl get pods -n web-ui -l "app.kubernetes.io/name=kubernetes-dashboard,app.kubernetes.io/instance=kubernetes-dashboard" -o jsonpath="{.items[0].metadata.name}")
	kubectl -n web-ui port-forward $POD_NAME 8443:8443
	```

1.	Use any web-browser to access "https://localhost:8443", kindly ignore the certificate error.

1.	Login with "kube config" file from your c:\users\YOURNAME\.kube folder.

1.	Explore the dashboard.