Smallest deployable unit of computing

Group of one or more containers with shared storage and network resources and specification on how to run the container.

Designed as ephemeral disposable entities. When pod gets created, the pod is scheduled to run on [[K8S Worker Node]] in [[Cluster]]

Pods remain on [[K8S Worker Node]] until they finish execution/fail/get evicted. 

Usually you don't create pods directly. You create the by using [[K8S workloads]] like [[K8S Deployment]] or [[K8S Job]]

Typically each pod is meant to run single instance of application. 

Each pod is meant to represent a single unit of deployment, and scaling horizontally

#flashcards/k8s
What is the smallest deployable unit in Kubernetes?::Pod

Pods are designed as ==ephemeral disposable== entities

How are Pods typically created?::Via workloads like Deployment or Job, rather than directly

Pod:::Smallest deployable unit of computing; a group of one or more containers with shared storage and network resources