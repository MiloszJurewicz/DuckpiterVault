Smallest deployable unit of computing

Group of one or more containers with shared storage and network resources and specification on how to run the container.

Designed as ephemeral disposable entities. When pod gets created, the pod is scheduled to run on [[K8S Worker Node]] in [[Cluster]]

Pods remain on [[K8S Worker Node]] until they finish execution/fail/get evicted. 

Usually you don't create pods directly. You create the by using [[K8S workloads]] like [[K8S Deployment]] or [[K8S Job]]

Typically each pod is meant to run single instance of application. 

Each pod is meant to represent a single unit of deployment, and scaling horizontally

---

#flashcards/k8s
What do all containers inside a Pod share?::Storage and network resources

Pods are designed as ==ephemeral disposable== entities — they get rescheduled rather than repaired

How are Pods typically created in practice?::Via higher-level workloads like Deployments or Jobs, not directly

Why scale horizontally with Pods rather than vertically?::Each Pod represents a single unit of deployment designed to run one instance of the application; you add more Pods to scale