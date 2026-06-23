#k8s 
Deployment provides declarative updates for [[K8S Pod]]s and [[K8S ReplicaSet]]s 

You **describe desired state** in a deployment and the [[K8S Deployment Controller]] changes the actual state to the desired state at a controlled rate. 

You can define Deployment to create new Replica sets or to remove existing

---

#flashcards/k8s
What does a Deployment manage? (two resource types)::Pods and ReplicaSets

You describe the ==desired state== and the Deployment Controller reconciles the actual state ==at a controlled rate==

A Deployment can be used to create new ReplicaSets or ==remove existing== ones

What does "declarative" mean in the context of a Deployment?::You specify the desired state and Kubernetes figures out how to reach it, rather than issuing step-by-step commands