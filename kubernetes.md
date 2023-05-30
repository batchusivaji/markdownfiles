........................................KUBERNETES........................
                                          
### 1) Write a Pod Spec for Spring PetClinic as well as nopCommerce Applications at the same spec EXPOSE ports spc & nop
ANS: first we create k8s pods like spc & nop
-------------------------------------------------------------------
 ```yml
apiVersion: v1
kind: Pod
metadata:
  name: spring-petclinic
spec:
  containers:
    - name: spc
      image: batchusivaji/raj:1.0
      ports:
        - containerPort: 8080
    - name: nop
      image: batchusivaji/rajshekar:1.0
      ports:
        - containerPort: 5000

```
Now we have to apply below commands
  * kubectl apply -f <manifest.yml>
  * kubectl get pods
  * kubectl get pods -o wide
  * kubectl describe pods (podname)
  * ![preview](images/k8s-1.png)
  * ![preview](images/k8s-2.png)
  * ![preview](images/k8s-3.png)
 
### 2). Write a Pod Spec for Spring PetClinic
-----------------------------------------------------------------------
```yml
apiVersion: v1
kind: Pod
metadata:
  name: spring-petclinic
spec:
  containers:
    - name: spc
      image: batchusivaji/raj:1.0
      ports:
        - containerPort: 8080
 ```
  ![preview](images/k8s-4.png)
  ![preview](images/k8s-5.png)
----------------------------------------------------------------------------
### gol
```yml
---
apiVersion: v1
kind: Pod
metadata:
  name: gameoflife
spec:
  containers:
    - name: gol
      image: batchusivaji/kishore:1.1
      ports:
        - containerPort: 8080
```
![preview](images/batch-2.png)

### Job manifest file
```yml
---
apiVersion: batch/v1
kind: Job
metadata:
  name: job
spec:
  backoffLimit: 2
  template:
    metadata:
      name: alpine
    spec:
      restartPolicy: Never
      containers:
        - name: nginx-job
          image: nginx
          ports:
            - containerPort: 80  
  ```
![preview](images/batch-1.png)
###  Write a Pod Spec for nopcommerse
```yml
apiVersion: v1
kind: Pod
metadata:
  name: nopcommerse
spec:
  containers:
    - name: spc
      image: batchusivaji/rajshekar:1.0
      ports:
        - containerPort: 5000
 ```
  * kubectl apply -f <nop.yml>
  * kubectl get pods
  * kubectl get pods -o wide
  * kubectl describe pods (podname)
  
  ![preview](images/k8s-6.png)
  ![preview](images/k8s-7.png)

### GAME OF LIFE
first we create k8s pods like gol 
```yml
apiVersion: v1
kind: Pod
metadata:
  name: game of life
spec:
  containers:
    - name: gol
      image: batchusivaji/kishore:1.1
      ports:
        - containerPort: 8080
```
  * kubectl apply -f <gol.yml>     - 
  * kubectl get pods
  * kubectl get pods -o wide
  * kubectl describe pods (podname)
  * kubectl delete pods --all
  ![preview](images/k8s-9.png)
  ![preview](images/k8s-10.png)
## Restart Polices
### Restart Always
```yml
---
apiVersion:	v1
kind: Pod	
metadata:
  name: restartalways
spec:
  restartPolicy: Always
  containers:
    - name: jenkins
      image: jenkins/jenkins:jdk11-hotspot-windowsservercore-2019
      args:
        - sleep
        - 10s
```
![preview](images/restart-2png.png)
### Restart Never
```yml
---
apiVersion:	v1
kind: Pod	
metadata:
  name: restarnever
spec:
  restartPolicy: Never
  containers:
    - name: gameoflife
      image: batchusivaji/kishore:1.1
      args:
        - sleep
        - 1d
  ```
  ![preview](images/restart-3.png)
### Restart Onfailure
```yml
---
apiVersion:	v1
kind: Pod	
metadata:
  name: restarnever
spec:
  restartPolicy: Never
  containers:
    - name: gameoflife
      image: batchusivaji/kishore:1.1
      args:
        - sleep
        - 1d
```
![preview](images/restart-4.png)

-----------------------------------------------------------------
## REPLICASET manifest file
 * kubectl apply -f <replicaset.yml>     - 
  * kubectl get pods
  * kubectl get pods -o wide
  * kubectl describe pods (podname)
  * kubectl delete pods --all

```yml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  labels: 
    app: alpine
  name: alpine
spec:
  minReadySeconds: 2
  replicas: 3
  selector: 
    matchLabels: 
      app: 'alpine'
  template: 
    metadata:
      labels: 
        app: alpine
    spec:
      containers:
        - name: alpine
          image: alpine
          args:
            - sleep 
            - 1s
```
![preview](images/k8s-14.png)
![preview](images/replicasets-1.png)
![preview](images/replicasets-2.png)
![preview](images/replicasets-3.png)


--------------------------------
  ### restart always manifest file
  
  ```yml
apiVersion:	v1
kind: Pod	
metadata:
  name: restartalways
spec:
  restartPolicy: Always
  containers:
    - name: jenkins
      image: jenkins/jenkins:jdk11-hotspot-windowsservercore-2019
      args:
        - sleep
        - 10s

  ```
![preview](images/k8s-11.png)
![preview](images/k8s-12.png)
![preview](images/k8s-12.png)
----------------------------------------------------------------------------
### Restart never

```yml
apiVersion:	v1
kind: Pod	
metadata:
  name: restarnever
spec:
  restartPolicy: Never
  containers:
    - name: gameoflife
      image: batchusivaji/kishore:1.1
      args:
        - sleep
        - 1d 

```
![preview](images/k8s-16.png)
![preview](images/k8s-17.png)

### CronJob
```yml
apiVersion: batch/v1
kind: CronJob
metadata:
  name: cronob-labels
  labels:
    app: lebel-redis
spec:
  schedule: 1 * * * *
  jobTemplate:
    metadata:
      name: cronob-labels
      labels:
        app: label-redis
    spec:
      template:
        metadata:
          labels:
            app: label-redis
          name: cronob-labels
        spec:
          restartPolicy: OnFailure
          containers:
            - name: spc
              image: redis:7.2 
              args:
                - sleep
              command:
                - 10s

  
```
![preview](images/k8s-18.png)
![preview](images/cron.png)
![preview](images/k8s-19.png)
![preview](images/k8s-20.png)
![preview](images/k8s-21.png)
![preview](images/k8s-22.png) 
![preview](images/k8s-29.png)


### Replication controller

```yml
apiVersion: v1
kind: ReplicationController
metadata:
  name: replication-controller
  labels:
    app: redis
spec:
  minReadySeconds: 2
  replicas: 2
  selector:
    app: redis                
  template:
    metadata:
      labels:
        app: redis
    spec:
      containers:
        - name: redis
          image: redis
          args:
            - sleep
            - 10s
 ```
 ![preview](images/k8s-23.png)
 ![preview](images/k8s-24.png)
### Imperative way
![preview](images/imperative.png)

 ### Match-expressions using manifest file
 ```yml
apiVersion:	apps/v1
kind: ReplicaSet
metadata:
  name: setbased
  labels: # label is not reqired
    app: redis
spec:
  minReadySeconds: 2
  replicas: 2
  selector: # to set based selector , can be used to select multiple options in single selection
    matchExpressions:
      - key: app
        operator: In
        values:
          - apache2
          - nginix
      - key: dev
        operator: NotIn
        values:
          - linux
          - unix
  template:
    metadata:
      name: match-expressions
      labels:
        app: apache2 # this spec is used in selector
        dev: developer
    spec: 
      containers:
        - name: redis
          image: redis:7.2
          args:
            - sleep
          command:
            - 10s
```
![preview](images/k8s-25.png)
![preview](images/k8s-26.png)
![preview](images/k8s-27.png)
![preview](images/k8s-28.png)


### LoadBalancer :
this Service exposes a set of pods using an external load balancer. All managed Kubernetes offerings have their own implementation of it
![preview](images/k8s-40.png)
![preview](images/loadbalancer.png)
### NodePort : 
the Service exposes a given port on each Node IP in the cluster.
![preview](images/k8s-38.png)
![preview](images/k8s.41.png)
### Ingress:  
NodePort and LoadBalancer let you expose a service by specifying that value in the service’s type. Ingress, on the other hand, is a completely independent resource to your service. You declare, create and destroy it separately to your services.

This makes it decoupled and isolated from the services you want to expose. It also helps you to consolidate routing rules into one place.

The one downside is that you need to configure an Ingress Controller for your cluster. But that’s pretty easy—in this example, we’ll use the Nginx Ingress Controller.
![preview](images/ingress%201.png)

### Liveness and Readiness probe
```yml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: jenkis-sever-healthchecks
  labels:
    app: server
spec:
  minReadySeconds: 1
  replicas: 2
  selector:
    matchExpressions:
      - key: developer
        operator: In
        values:
          - web
          - dev
      - key: tester
        operator: NotIn
        values:
          - qt
          - ihub
  template:
    metadata:
      name: qualityThought
      labels:
        developer: dev
        tester: deploy 
    spec:
      containers:
        - name: jenkins
          image: jenkins/jenkins:2.387.3-lts
          ports:
            - containerPort: 8080
              protocol: TCP
          readinessProbe:
            failureThreshold: 1
            initialDelaySeconds: 1
            periodSeconds: 10
            successThreshold: 2
            timeoutSeconds: 1
            exec:
              command:
                - sleep
                - 10mb
          livenessProbe:
            failureThreshold: 2
            initialDelaySeconds: 1
            periodSeconds: 10
            successThreshold: 1
            timeoutSeconds: 1
            exec:
              command:
                - sleep
                - 5s
```
![preview](images/k8s-32.png)
![preview](images/k8s-33.png)
![preview](images/k8s-34.png)
![preview](images/k8s-35.png)
`
### pod:
Collections of containers collocated in a single machine

### Service:
Load balancer that can bring traffic to a collection of pods

### Deployment:
Replicate a container for availability or scale.

### Kubelet:
The primary node agent that runs on each node

# What is Kubernetes?
Kubernetes is an orchestrator for containers like Swarm, runs on top of Docker usually as a set of APIs in containers.

Provides API or CLI to manage container across servers.

Many clouds provide it for you.

Many vendors make a "distribution" of it.

# System parts:
### Kubernetes:
The whole orchestratuion system
### Kubectl:
CLI to manage Kubernetes and manage apps.
### Node:
Single server in the Kubernetes cluster.
### Kubelet:
Kubernetes agent running on nodes.
### Control Plane:
Set of containers that manage the cluster.
### Pods:
Basic unit of deployment, containers are always in pods.
### Controller: 
For creating/updating pods and other objects.
### Service: 
Endpoint to connect to a pod.
### Namespace: 
Filtered group of objects in cluster.

Creating pods with kubectl
First, be sure kubernetes its running:

kubectl version

### Two ways to deploy Pods(containers): via CLI or via YAML.

### Scaling a ReplicaSet:
Example of scaling an existing Apache server replica:

kubectl scale deploy/my-apache --replicas 2
or
kubectl scale deployment my-apache --replicas 2

Inspecting Deployment Objects
Showing your pods:

kubectl get pods

# Basic Service Types:
### ClusterIP (default):
Single, internal virtual IP allocated.
Only reachable within the cluster (nodes and pods).
Pods can reach service on apps port number.
### NodePort:
High port allocated on each node.
Port it's open on every node's IP.
Anyone can connect (if they can reach node).
Other pods need to be updated to this port.
These services are always available in Kubernetes.
### ReplicationController:
High availability
Scaling can be done
Loadbalancing setup
Adding your pod to ReplicationController will make sure to create new/multiple replicas of pod automatically.

### What is Kubernetes?
In simple terms, Kubernetes is a container orchestration tool. It helps in maintaining the containers.

When we build a containerized application and if there are large number of such containers, we need tool such as Kubernetes that help us to manage those containers and automate our workflow.

# What features does Kubernetes provides?
### High Availability : 
The user should not have any downtime.
### Scalability: 
the application normally have very high response time.
### Disaster Recovery :
 backup and restore.
# Kubernetes basic terminologies
### Pods: 
Pods are the smallest and the most basic unit in Kubernetes. Each pod get their own IP address so that they can communicate. A pod may be running a service like any application usually within a container.
### Service: 
Service is logical set of pods and each pod will have their own service. Lifecycle of Pod and service are not interconnected. Service are generally categorized into:
Internal
External
### Node : 
A node is a single host in K8s. This is used to run virtual or physical machine. There may be multiple/single pods within a node.
### ReplicaSet:
It is used to identify the particular number of pod replicas running inside a node.
### ConfigMap :
It contains all the external configuration of our application like database URL. The reason we need this is because this acts as a central repo to other components so if we have to make any changes like change in DB_URL we can simply change here and all changees will be reflected back.
⚠ DO NOT STORE CREDENTIALS ON CONFIGMAP.
### Secret:
As name suggests it stores all the secret info like DB_USERNAME and DB_PASSWORD. We should always store such info in encrypted format rather than plain text.
### Volumes: 
This attaches a physical storage to the pod. Data mey be lost while resetting since it is not persistent.
⚠ K8s does not manage data persistence.
### Deployment:
 We do not directly create a pod in K8s. We create blueprint of the pod and the rest is handled by K8s. The blueprint for creating pod is called deployment.

### initcontainer

```yml
---
apiVersion:	v1
kind: Pod
metadata:
  name: initcontainers
  labels:
    run: webapp       
spec:
  containers:
    - name: nginx
      image: nginx:latest
      ports:
        - containerPort: 80 
  initContainers:
    - name: alpine
      image: alpine:latest
      args:
        - sleep
        - 15s
    - name: busybox
      image: busybox:1.28
      command:
        - 'sh' 
        - '-c'
        - "until nslookup nginx-svf.default.svc.cluster.local; do echo waiting for myservice; sleep 2; done"
       
  #### service file

  ---
apiVersion: v1
kind: Service
metadata:
  name: nginx-svf
  labels:
    run: nginx
spec:
  ports:
    - name: nginx
      port: 80
      protocol: TCP
      targetPort: 35000
  selector:
    run: nginx
```
  ![preview](images/k8s-43.png)
  ![preview](images/k8s-44.png)
  ![preview](images/k8s-45.png)
### Run pod with specific resourses
```yml
apiVersion: apps/v1
kind: ReplicaSet 
metadata:
  name: nginx-pod
  labels:
    run: pod
spec:
  minReadySeconds: 2
  replicas: 3
  selector:
    matchLabels:
      app: test
  template:
    metadata:
      name: nginx
      labels:
        app: test
    spec:
      containers:
        - name: nginx
          image: latest
          ports:
            - containerPort: 80
          livenessProbe:
            httpGet:
              path: /
              port: 80
          readinessProbe:
             httpGet:
               path: /
               port: 80
          resources:
            requests:
              memory: "64Mi"
              cpu: "256m"
            limits:
              memory: "256Mi"
              cpu: "1000m"
              
---
apiVersion: v1
kind: Service
metadata:
  name: nginx-svf
  labels:
    run: nginx
spec:
  ports:
    - name: nginx
      port: 80
      protocol: TCP
      targetPort: 35000
  selector:
    run: nginx
    
```
![preview](images/k8s-47.png)
![preview](images/k8s-48.png)
![preview](images/k8s-49.png)
![preview](images/k8s-50.png)
![preview](images/k8s-51.png)

### rollout-rollback
```yml
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: deployment
  labels:
    run: server
spec: 
  minReadySeconds: 5
  replicas: 2
  selector:
    matchExpressions:
      - key: qat
        operator: In
        values:
          - test
          - pause

      - key: dev
        operator: NotIn
        values:
          - deploy
          - failure
  strategy:
    rollingUpdate:
      maxSurge: 2
      maxUnavailable: 1
  template:
    metadata:
      name: pod-creation
      labels:
        qat: test
        dev: env
    spec:
      containers: 
        - name: httpd-service
          image: httpd:2.4.57
          ports:
            - containerPort: 80
  
```
![preview](images/k8s-52.png)
![preview](images/k8s-53.png)
![preview](images/k8s-54.png)
![preview](images/k8s-55.png)
![preview](images/k8s-56.png)

## RBAC(role base access control)
### role &role binding
```yml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata: 
  name: qat-dev
  namespace: dev
rules:
  - apiGroups: ["*"]
    resources: [ pods ]
    verbs: 
      - get
      - watch
      - creat
```yml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata: 
  name: qat-dev
  namespace: dev
rules:
  - apiGroups: ["*"]
    resources: [ pods ]
    verbs: 
      - get
      - watch
      - creat
```
![preview](images/k8s-57.png)
![preview](images/k8s-58.png)
![preview](images/k8s-59.png)
![preview](images/k8s-60.png)

## kustamization

### deployment manifest file

```yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  namespace: dev
  labels:
    app: nginx
spec:
  minReadySeconds: 4
  replicas: 1
  selector:
    matchLabels:
      app: nginx
  strategy:
    rollingUpdate:
      maxSurge: 2
      maxUnavailable: 1
    type: RollingUpdate
  template:
    metadata:
      name: nginx
      labels:
        app: nginx
    spec:
      containers:
        - name: nginx
          image: nginx:1.23.4-perl
          ports:
            - containerPort: 80


  ```
  ### service manifest file
  ```yml
apiVersion: v1
kind: Service
metadata:
  name: nginx
  labels:
    app: nginx
spec:
  selector:
    app: nginx
  ports:
    - port: 80
      protocol: TCP
      targetPort: 32000
  type: LoadBalancer

  ```
  ### horizontal pod autoscaling manifest file
  ```yml
  apiVersion: autoscaling/v1
kind: HorizontalPodAutoscaler
metadata:
  name: nginx
  namespace: dev
spec:
  maxReplicas: 8
  minReplicas: 2
  scaleTargetRef:
    kind: deployment
    name: dev
  targetCPUUtilizationPercentage: 65

  ```
  ### kustomization manifest file
  ```yml
apiVersion: kustomize.config.k8s.io/v1beta1
kind: Kustomization
namespace: dev
resources:
  - deployment.yml
  - horizontal-pod-autoscaling.yml
  - service.yml
  - namespace.yml
``` 
### namespace manifest file
```yml
apiVersion: v1
kind: Namespace
metadata:
  name: dev

  ```
  ![preview](images/k8s-61.png)
  ![preview](images/k8s-64.png)
  ![preview](images/k8s-62.png)
  ![preview](images/k8s-65.png)
  ![preview](images/k8s-66.png)


  ## horizontal pod auto scalling(hpa)
```yml
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx
  labels:
    run: nginx
spec: 
  minReadySeconds: 3
  replicas: 2 
  selector:
    matchExpressions:
      - key: qat
        operator: In
        values:
          - test
          - pause

      - key: dev
        operator: NotIn
        values:
          - deploy
          - failure
  strategy:
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 1
  template:
    metadata:
      name: pod-creation
      labels:
        qat: test
        dev: env
    spec:
      containers: 
        - name: nginx
          image: nginx:1.23
          ports:
            - containerPort: 80
          resources:
            requests:
              memory: "64Mi"
              cpu: "250m"
            limits:
              memory: "80Mi"
              cpu: "500m"

---
apiVersion: v1
kind: Service
metadata:
  name: nginx
spec:
  selector:
    run: nginx
  ports:
    - name: nginx
      port: 80
      protocol: TCP
      targetPort: 35000
  
```
  hpa has maintaining the pods there are two types of pods maintaining pod
  * we have to manifest
  * we have to pass the commanand
  * after that we have to apply below command
      kubectl apply -f mainifest file name
  * we have to create the hpa 
    `kubectl autoscale deployment nginx --cpu-percent=50 --min=1 --max=10` 
     then we have to check the hpa `kubectl get hpa`
  * then after that we have to increase or scaling the load
     `kubectl scale --replicas=10 -f <mainifest file name>`
  * we have to check the pods then we will automatically increase the pods
   it will depend on the cpu percentage after that we have to enter `cntrl+C` 
   then automatically decrease the pods that means killing the rs or pods
  
      `kubectl get hpa nginx --watch`


![preview](images/hpa-1.png)
![preview](images/hpa-2.png)
![preview](images/hpa-3.png)
![preview](images/hpa-4.png)