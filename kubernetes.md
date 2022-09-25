
### commands
```
kubectl get deployments
kubectl get rs
kubectl api-resources
kubectl get po
kubectl get pods -o wide
kubectl get rc,services
kubectl get node
kubectl cluster-info
kubectl describe deployment
kubectl get pods --field-selector=status.phase=Pending
kubectl describe pod postgres-89784f745-6nq8s
kubectl uncordon docker-desktop
```


### Fix - pending schedule
```
stelios@LAPTOP-NCMTS5FG:/mnt/d/fc/fetchcombo-stack/deployment$ kubectl get pods --field-selector=status.phase=Pending
NAME                          READY   STATUS    RESTARTS   AGE
postgres-89784f745-6nq8s      0/1     Pending   0          47h
search-api-68944cbd6f-2fxnh   0/1     Pending   0          47h
web-956665594-pfnfc           0/1     Pending   0          47h
web-api-68f979b47-2km5j       0/1     Pending   0          47h
stelios@LAPTOP-NCMTS5FG:/mnt/d/fc/fetchcombo-stack/deployment$ kubectl describe pod postgres-89784f745-6nq8s
Name:             postgres-89784f745-6nq8s
Namespace:        default
Priority:         0
Service Account:  default
Node:             <none>
Labels:           app=postgres
                  app.kubernetes.io/managed-by=tilt
                  pod-template-hash=89784f745
                  tilt.dev/pod-template-hash=5a5dfa16127a5ce98a8a
Annotations:      <none>
Status:           Pending
IP:
IPs:              <none>
Controlled By:    ReplicaSet/postgres-89784f745
Containers:
  postgres:
    Image:      postgres:14.4
    Port:       5432/TCP
    Host Port:  0/TCP
    Environment Variables from:
      postgres-secret  ConfigMap  Optional: false
    Environment:       <none>
    Mounts:
      /var/lib/postgresql/data from postgresdata (rw)
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-vwl76 (ro)
Conditions:
  Type           Status
  PodScheduled   False
Volumes:
  postgresdata:
    Type:       PersistentVolumeClaim (a reference to a PersistentVolumeClaim in the same namespace)
    ClaimName:  postgres-volume-claim
    ReadOnly:   false
  kube-api-access-vwl76:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    ConfigMapOptional:       <nil>
    DownwardAPI:             true
QoS Class:                   BestEffort
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:                      <none>
stelios@LAPTOP-NCMTS5FG:/mnt/d/fc/fetchcombo-stack/deployment$ kubectl get node
NAME             STATUS                     ROLES           AGE   VERSION
docker-desktop   Ready,SchedulingDisabled   control-plane   8d    v1.25.0
stelios@LAPTOP-NCMTS5FG:/mnt/d/fc/fetchcombo-stack/deployment$ kubectl uncordon docker-desktop
node/docker-desktop uncordoned
stelios@LAPTOP-NCMTS5FG:/mnt/d/fc/fetchcombo-stack/deployment$ kubectl get pods --field-selector=status.phase=Pending
No resources found in default namespace.
stelios@LAPTOP-NCMTS5FG:/mnt/d/fc/fetchcombo-stack/deployment$ kubectl get pods
NAME                          READY   STATUS    RESTARTS   AGE
postgres-89784f745-6nq8s      1/1     Running   0          47h
search-api-68944cbd6f-2fxnh   1/1     Running   0          47h
web-956665594-pfnfc           1/1     Running   0          47h
web-api-68f979b47-2km5j       1/1     Running   0          47h
```
