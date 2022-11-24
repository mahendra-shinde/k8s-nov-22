# Kubernetes Secrets

- Similar to ConfigMap, used for storing environment variables or configuration for application.
- Value are `Base64` encoded, when `Passed to Containers` kubernetes will Decode them.
- Secrets are of THREE types

	Kind | Description
 	--------------|---------------------------
	Generic Secret | Just like ConfigMaps, Key/Value pairs
	Docker Registry | Special secret that contains registry credentials
	TLS | Digital Certificates
	
	

## Generic Secret from Kubectl Command

```
kubectl create secret generic mysecrets --from-literal=name=mahendra --from-literal=city=mumbai
kubectl describe secret mysecrets
kubectl get secret mysecrets -o yaml
```

## Docker Registry Secret

```
kubectl create secret docker-registry reg-secret --docker-username=mahendrashinde --docker-password=fcPeunDVr+ii1Y3xr+5d5gluVJH4w1Tg --docker-server=mahendrashinde.azurecr.io

kubectl describe secret reg-secret
```

## Pod that uses both secrets

- Registry Secret is injected as follows:

	```yaml
	imagePullSecrets:
	- name: reg-secret
	```

- Generic Secret is injected as Environment Variables

	```yaml
	  envFrom:
	    - secretRef:
	      name: mysecrets
	```