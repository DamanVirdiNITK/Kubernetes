# Kubernetes
1. To create single container in a pod -> singlecontainerinpod.yml</br>
2. To create multiple container in a pod -> multiplecontainerinPod.yml</br>
3. Set enviornment variables for container -> enviornmentVariable.yml </br>
4. Set labels to the pods -> label.yml </br>
5. Set Node Selector for pods -> NodeSelector.yml</br>

## To create the container, service, namespace etc via yaml file
kubectl apply -f pod.yml </br>
pod/damanpod created</br>

## To view pods
kubectl get pods</br>
NAME                READY   STATUS             RESTARTS        AGE</br>
damanpod            1/1     Running            0               11s

## To view more info about pods
kubectl get pods -o wide</br>
NAME                READY   STATUS             RESTARTS        AGE     IP              NODE               NOMINATED NODE   READINESS GATES</br>
damanpod            1/1     Running            0               29s     192.168.85.28   ip-172-31-17-220   <none>           <none></br>

## To see details and lifecycle of pod
 kubectl describe pod <podname></br>

 ## To see what is the o/p or happening inside the container
 kubectl logs -f <podname> <containername></br>

 ## To go inside the running container
 kubectl exec <podname> -it -c <cont name> -- /bin/bash</br>
 exit to come out of it

 ## To see all containers in the pods


## To set pod enviornment variables
execute enviornmentVariable.yml</br>
go inside the container</br>
IP: echo $state</br>
OP: production</br>

## To set Labels to the pods
1. add labels to the existing pod</br>
   kubectl label pods testlabel env1 = development1</br>
2. change existing label of the pod</br>
   kubectl label pods testlabel env1=development2 --overwrite</br>
3. filter all the pod with env=prod
   kubectl get pods -l env=development --show-labels
4. filter all the pods with label not matching
   kubectl get pods -l env!=development --show-labels
5. filter all the pods in multiple labels
   kubectl get pods -l 'env in(development,develop)' --show-labels

##  Label the Node(NodeSelector)
1. To see the labels of the nodes</br>
    kubectl get nodes --show-labels</br>
2. To label the nodes</br>
    kubectl label nodes <node-name <ip-<ipof node>>> labelKey = labelValue

## 



   
