#k8s 
A machine that runs containers within the cluster
- Run actual workloads, containers inside of pods
- Runs and manages containers on the node
- Monitors the state of containers on the node and reports the status back to the [[K8S Control Plane]]

---

#flashcards/k8s
What are the three responsibilities of a Worker Node?::Run workloads (containers inside Pods), manage containers on the node, monitor and report container status back to the Control Plane
<!--SR:!2026-06-23,0,230-->

Worker Nodes report container health and status back to the ==Control Plane==
<!--SR:!2026-06-23,0,230-->

Where do Pods actually execute in the cluster?::On Worker Nodes