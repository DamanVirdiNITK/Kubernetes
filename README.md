# Kubernetes
1. To create single container in a pod -> singlecontainerinpod.yml</br>
2. To create multiple container in a pod -> multiplecontainerinPod.yml</br>
3. Set enviornment variables for container -> enviornmentVariable.yml </br>
4. Set labels to the pods -> label.yml </br>
5. Set Node Selector for pods -> NodeSelector.yml</br>
6. Create Replication Controller -> replicationController.yml</br>
7. Create namespace -> namespace.yaml</br>
8. Create pod in namespace -> singlecontainerinpod.yml</br>
9. Set request and limit of container in pod -> podresource.yml</br>
10. Create resource quota and pods, rc via deployment-> resourcequota.yml, resourceContainerDeployment.yaml</br>
11. Test horizontal Auto scaling using Metric Server -> deployhpa.yml

## To create the container, service, namespace etc via yaml file
kubectl apply -f pod.yml </br>
pod/damanpod created</br>

## To view pods
kubectl get pods</br>
NAME                READY   STATUS             RESTARTS        AGE</br>
damanpod            1/1     Running            0               11s

## To view more info about pods0
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
0
1. EMPTYDIR</br>
apply emptyDirMountVol.yml , go inside container 1, in the mentioned directory, create file</br>
go inside another container, in the mentioned directory, file will be present over there</br>

3. Persistent Volume - Abstracts of how storage is provided and from how it is consumed
    PV - Piece of storage in cluster
    PVC - Request for storage

   Lifecycle of a persistent Volume
   Provisioning --> Binding --> using --> Reclaiming

   Provisioning can be done at two levels -> Static - PV need to be created before PVC
                                             Dynamic - PV is created at same time of PVC 
    pending, will update soon

   

## Deployment
## Rollback
## Networking
## Services -ClusterIP &NodePort
## Scheduled Jobs - Cron Jobs
## Namespace

kubectl get namespace</br>
We'll create pods in namespaces. By default pods are created in <b>default</b> namespace</br>

kubectl apply -f singlecontainerinpod.yml -n <namespace></br>

kubectl get pods ---> No o/p beacuse it'll show the pods in default namespace only</br>
kubectl get pods -n <namespace> </br>

kubectl delete -f singlecontainerinpod.yml -> It will not delete the pod, because it won't be able to find the pod in default namespace</br>
kubectl delete -f singlecontainerinpod.yml -n <namespace></br>

Set dev as default namespace</br>, set any namespace as default</br>
kubectl config set-context $(kubectl config current-context) --namespace=dev</br>
Now, kubectl get pods -> It'll show the pods of this namespace only</br>

To check which is our default namespace</br>
kubectl config view | grep namespace:</br>


## Resource Quota & Limit
Task1:</br>
1. create the pod and defines in requests and limits in podresource.yml and then create it</br>

Task2:</br>

1. Create resource quota -> resourcequota.yml</br>
2. We create pods with 3 replicas in a deployment (via resourceContainerDeployment.yml), each requiring 200 m cpu, toatal 600m cpu, but we have defined max limit as 400m in resourcequota.yml,  so no pod will be create, replica set will be there stating DESIRED POD =3 and CURRENT POD = 0</br>

## Horizontal AutoScaling via Metric Server
Install metricserver</br>
wget -O metricserver.yml https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml</br>
vi metricserver.yml, go to line 134 and add the comment -- kubelet-insecure-tls</br>
kubectl apply -f metricserver.yml </br>
kubectl get pods -n kube-system</br>

apply deployhpa.yaml , it is having requests and limits for the resources</br>

How AutoScale happens?</br>
Metric Server send data to HPA, Whenever the CPU utilization will be more than 15% , request will go to deployment to create more pod</br>
kubectl autoscale deployment deployments --cpu-percent=15 --min=1 --max=10</br>

Open the master node from another another tab of AWS (to increase the traffic)</br>
do any activity inside that , update or install any package. </br>

## Security Context
defines priviliges for individual pods and containers
