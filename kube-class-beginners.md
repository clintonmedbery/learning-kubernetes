
## Beginner Class

### POD notes

`k get pods`
`k get pods -o wide`
`k run nginx --image nginx`
`k describe pod nginx`
`k run redis --image=redis --dry-run=client -o yaml > pod.yaml`

### Exec into Pod

`k exec -it hello-deployment-5d5845494-j2c6w -c hello-kubernetes -- /bin/bash`

### Get IPs for Pods
`kubectl get pods -l env=dev \      
    -o go-template='{{range .items}}{{.status.podIP}}{{"\n"}}{{end}}'`

### ReplicationController vs ReplicaSet
1. ReplicaSet replaces ReplicationController
1. ReplicaSet includes selectors.

https://www.devopsschool.com/blog/difference-between-replicaset-and-replicationcontroller/

`k get replicationcontroller`
'k get replicaset`
`k delete replicaset myapp-name`

How to update replicaset?

`k replace -f replicaset-definition.yaml`
`k scale --replicas=6 -f replicaset-definition.yaml`
`k scale --replicas=6 -f replicaset myapp-replicaset`
`k edit replicaset myapp-replicaset`

### Deployment 
1. Contains ReplicaSet but also can rollout deployments, which help with the transition of one deployment to another.

#### Create
`k apply -f deployment-definition.yaml`
`k apply -f deployment-definition.yaml --record`

#### Update
`k apply -f deployment-definition.yaml`
`k set image deployment/myapp-deployment nginx=nginx:1.9.1`
`k edit deployment myapp-deployment`


#### Get
`k get deployments`

#### Status
`k rollout status deployment/myapp-deployment`
`k rollout history deployment/myapp-deployment`

#### Undo
`k rollout undo deployment/myapp-deployment`

### Services
1. Services expose your inner pod to the outside world
1. > An abstract way to expose an application running on a set of Pods as a network service.
With Kubernetes you don't need to modify your application to use an unfamiliar service discovery mechanism. Kubernetes gives Pods their own IP addresses and a single DNS name for a set of Pods, and can load-balance across them.



`k apply -f service-definition.yaml`

##### Expose the port to your host computer

`kubectl port-forward service/myapp-service 3003:3000`