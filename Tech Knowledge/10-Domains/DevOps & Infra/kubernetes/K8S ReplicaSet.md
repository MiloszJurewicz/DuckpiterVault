A **ReplicaSet** in Kubernetes ensures that a specified number of identical [[K8S Pod]] replicas are always running.

---

#flashcards/k8s
What does a ReplicaSet guarantee?::That a specified number of identical Pod replicas are always running

If a Pod in a ReplicaSet fails, what happens?::The ReplicaSet automatically replaces it to maintain the desired replica count

Self-healing via replacement:::ReplicaSet