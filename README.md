# Kubernetes
1. To create single container in a pod -> singlecontainerinpod.yml</br>
2. To create multiple container in a pod -> multiplecontainerinPod.yml</br>
3. Set enviornment variables for container -> enviornmentVariable.yml </br>
4. Set labels to the pods -> label.yml </br>
5. Set Node Selector for pods -> NodeSelector.yml</br>
6. Create Replication Controller -> replicationController.yml</br>

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

## Replication Controller
1. To see all the replication controllers</br>
   kubectl get rc</br>
2. delete one pod (but new pod will be created again in its place)</br>
   kubectl delete pod <podname></br>
3. To scale up/ down no of replicas</br>
   kubectl scale --replicas = 10/1 rc -l labelkey=labelvalue</br>
4. To delete the replication controller</br>
   kubectl delete -f replicationController.yml</br>

## Mount Volume
1. EmptyDir - in same pod</br>
2. Hostpath  -in same node, but can be between different pods</br>
3. Persistent Volume - amongst multiple nodes</br>

1. EMPTYDIR</br>
apply emptyDirMountVol.yml , go inside container 1, in the mentioned directory, create file</br>
go inside another container, in the mentioned directory, file will be present over there</br>

3. Persistent Volume - pending, will update soon

## Deployment
## Rollback
## Networking
## Services -ClusterIP &NodePort
## Scheduled Jobs - Cron Jobs
## Namespace

kubectl get namespace</br>
We'll create pods in namespaces
## Resource Quota & Limit
## Horizontal AutoScaling
## Metric Server
   
