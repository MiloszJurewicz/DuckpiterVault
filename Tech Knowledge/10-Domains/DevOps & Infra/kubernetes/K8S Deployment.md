#k8s 
Deployment provides declarative updates for [[K8S Pod]]s and [[K8S ReplicaSet]]s 

You **describe desired state** in a deployment and the [[K8S Deployment Controller]] changes the actual state to the desired state at a controlled rate. 

You can define Deployment to create new Replica sets or to remove existing

---

#flashcards/k8s
What does a Deployment manage? (two resource types)::Pods and ReplicaSets
<!--SR:!2026-06-24,1,230-->

You describe the ==desired state== and the Deployment Controller reconciles the actual state ==at a controlled rate==
<!--SR:!2026-06-23,0,230!2000-01-01,1,250-->

A Deployment can be used to create new ReplicaSets or ==remove existing== ones

What does "declarative" mean in the context of a Deployment?::You specify the desired state and Kubernetes figures out how to reach it, rather than issuing step-by-step commands
<!--SR:!2026-06-26,3,250-->