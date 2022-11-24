## Kubernetes Storage /  Volume

Two Kinds Volumes / Storage in Kubernetes

1. Local Volumes used for temporary file-system. Can be accessed from multiple nodes

1. Persistent Volumes, are external storage services. Has 4 Access modes:

    - ReadWriteOnce [RWO]
    - ReadWriteMany [RWX]
    - ReadOnlyMany  [ROX]
    - ReadWriteOncePod [RWOP]

1. Local Volumes

	- EmptyDir
	
		```yml
		  volumes:
		  - name: logvolume
			emptyDir:
			  sizeLimit: 100Mi
		```

	
	- HostPath

		```yml
		  volumes:
		  - name: logvolume
			hostPath:
			  path: /var/dir1
		```

## EmptyDir Demo

```
kubectl apply -f 04-volume-pod-1.yml
kubectl describe -f 04-volume-pod-1.yml
kubectl delete -f 04-volume-pod-1.yml
```

