MetalLB is a load balancer implementation for bare-metal Kubernetes clusters. It provides network load-balancing functionality similar to what cloud providers offer, but for environments without built-in load balancers.

It works by assigning external IP addresses to [[K8S Service]] of type `LoadBalancer`. These IPs come from configured IP address pools defined by the cluster administrator.

An IP pool is a predefined range of IP addresses that MetalLB is allowed to allocate. When a [[K8S Service]] requests a LoadBalancer IP, MetalLB selects an available address from the pool and assigns it to that Service. The IP remains associated with the Service until it is deleted or the allocation is changed.

MetalLB operates mainly in two modes: Layer 2 mode and [[BGP]] mode. In [[Layer 2]] mode, it advertises the selected IP on the local network. In [[BGP]] mode, it announces routes to upstream routers using [[BGP]].