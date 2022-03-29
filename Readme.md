# Step
1. install kubectl
2. install minikube
3. `minikube start --driver=virtualbox`
4. check minikube status (command : minikube status)
5. `minikube dashboard --url`
   start example: `kubectl create deployment hello-node --image=k8s.gcr.io/echoserver:1.4`
6. expose as a service:
   `kubectl expose deployment hello-node --type=NodePort --port=8080`
   `minikube service hello-node --url`
7. delete:
   `kubectl delete deployment hello-node`
   `kubectl delete service hello-node`

# start with file
`kubectl create -f <filename>`

`kubectl get replicationcontroller`

`kubectl get replicaset`

# update edited replica definition

`kubectl replace -f replicaset-definition.yaml`

# provide new number of replica

`kubectl scale --replicas=6 -f replicaset-definition.yaml`

## alternative

`kubectl scale --replicas=6 replicaset <replicaset_name>`

deployment :

- deploy multiple app
- upgrade docker instance seamslessly (rolling update, one by one)
- roll back change
- multiple change rolled out one by one

when create a deployment, it triggers rollout, creates a new deployment revision.
kubectl rollout status deployment/hello-node
kubectl rollout history deployment/hello-node

undo rollout
kubectl rollout undo deployment/hello-node

update deployment
kubectl set image deployment/deployment_name image_name=image_nameversion


# Kubernetes Networking
i.e. :node ip 192.168.1.2 
- kubernetes create internal private network, then pod attached to the network
- need to modify networking by ourself to connect between pod

# Kubernetes Service

## command
`kubectl get services`
## types
- nodeport : portforwarding a pod port to node port
- clusterip : create virtual ip inside the cluster to enable connection between services (node)
- load balancer

## Nodeport
1. targetport: current running port of application
2. port : service object port attached to targetport (running application)
3. nodeport: port for extrenal access (30000-32767)
