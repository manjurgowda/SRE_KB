kubernetes documents and test codes


Kubernetes Cluster
│
├── Cluster-Level Resources (Global Scope)
│   │
│   ├── Nodes
│   │   ├── Worker Nodes
│   │   └── Control Plane Nodes
│   │
│   ├── Namespaces (Logical Isolation Boundary)
│   │   ├── default
│   │   ├── kube-system
│   │   ├── kube-public
│   │   └── custom namespaces (dev, prod, staging)
│   │
│   ├── RBAC (Access Control)
│   │   ├── ClusterRole
│   │   ├── ClusterRoleBinding
│   │
│   ├── Networking (Cluster-wide)
│   │   ├── NetworkPolicy
│   │   ├── IngressClass
│   │
│   ├── Storage (Cluster scope)
│   │   ├── StorageClass
│   │   ├── PersistentVolume (PV)
│   │
│   ├── Scheduling / Priority
│   │   ├── PriorityClass
│   │
│   └── Custom Resources
│       ├── CustomResourceDefinition (CRD)
│       └── Operators
│
│
├── Namespace-Level Resources (Isolated per Namespace)
│   │
│   ├── Workloads (Core Apps)
│   │   ├── Pod
│   │   ├── Deployment
│   │   ├── ReplicaSet
│   │   ├── StatefulSet
│   │   ├── DaemonSet
│   │   ├── Job
│   │   └── CronJob
│   │
│   ├── Networking
│   │   ├── Service
│   │   │   ├── ClusterIP
│   │   │   ├── NodePort
│   │   │   └── LoadBalancer
│   │   ├── Ingress
│   │   └── Endpoint / EndpointSlice
│   │
│   ├── Configuration
│   │   ├── ConfigMap
│   │   └── Secret
│   │
│   ├── Storage (Namespace binding)
│   │   ├── PersistentVolumeClaim (PVC)
│   │
│   ├── RBAC (Namespace scope)
│   │   ├── Role
│   │   ├── RoleBinding
│   │   └── ServiceAccount
│   │
│   ├── Autoscaling
│   │   ├── HorizontalPodAutoscaler (HPA)
│   │
│   ├── Policy & Security
│   │   ├── PodSecurityPolicy (deprecated → replaced by PSA)
│   │   ├── PodDisruptionBudget (PDB)
│   │
│   └── Observability / Misc
│       ├── Event
│       └── LimitRange
│       └── ResourceQuota
│
│
└── Underlying Relationships (Flow View)
    │
    ├── Deployment → ReplicaSet → Pod
    ├── StatefulSet → Pod (stable identity)
    ├── DaemonSet → Pod (one per node)
    ├── Job → Pod (batch execution)
    │
    ├── Service → Pod (via labels/selectors)
    ├── Ingress → Service → Pod
    │
    ├── PVC → PV → StorageClass
    │
    ├── HPA → Deployment/StatefulSet
    │
    └── RoleBinding → Role → ServiceAccount → Pod


🔹 Visual Mental Model

[ Cluster ]
   ├── [ Namespace: dev ]
   │       ├── Deployment
   │       ├── Service
   │       ├── ConfigMap
   │
   ├── [ Namespace: prod ]
   │       ├── StatefulSet (DB)
   │       ├── Service
   │
   └── [ Shared ]
           ├── Nodes
           ├── PVs
           ├── StorageClass
