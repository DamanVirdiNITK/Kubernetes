# Kubernetes
1. To create single container in a pod


## To create the container, service, namespace etc via yaml file
kubectl apply -f pod.yml 
pod/damanpod created

## To view pods
kubectl get pods
NAME                READY   STATUS             RESTARTS        AGE
damanpod            1/1     Running            0               11s

## To view more info about pods
kubectl get pods -o wide
NAME                READY   STATUS             RESTARTS        AGE     IP              NODE               NOMINATED NODE   READINESS GATES
damanpod            1/1     Running            0               29s     192.168.85.28   ip-172-31-17-220   <none>           <none>

## To see details and lifecycle of pod
 kubectl describe pod <podname>

 ## To see what is the o/p or happening inside the container
 kubectl logs -f <podname> <containername>

 ## To go inside the running container
 kubectl exec <podname> -it -c <cont name> -- /bin/bash
 exit to come out of it

 ## To see all containers in the pods

 
