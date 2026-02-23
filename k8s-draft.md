# Getting started: Kubernetes
Kubernetes is a container orchestration platform that allows us to manage and scale containerized applications across a cluster of machines.


In S3DF, it is the primary means of getting your application or service running on our infrastructure. This is achieved via a declarative approach (i.e., a set of yaml files that describes the desired 'deployment state' of your application) that abstracts away the underlying infrastructure. 


## How do I get started?
S3DF hosts a set of 90 vclusters across 9 facilities; access to these vclusters is available through Gangway and your SLAC account.

1. Request access to a vcluster? 
Each vcluster has a Gangway login page following the convention: `https://k8s.slac.stanford.edu/<vcluster_name>`. To gain access, or setup, a vcluster  submit a ticket to `s3df-help@slac.stanford.edu` (see `[LinkTo:`How to request a Kubernetes Environment`]` on specific info to include in the ticket). 


Gangway is an IdP proxy that allows you to authenticate using your SLAC account via a web portal. 

2. Once you have authenitcated on Gangway, you can connect using the Gangway's generated kubectl configurations and token. 

`Keep in mind that the token is only valid for 10 hours`. 
- To update the token after expiry: logout and login again to get a new token.

3. Once you are connected to the vcluster, you can use `kubectl` to interact with the Kubernetes API and deploy your applications. 


##### Overview of the process:
```
┌─────────────┐
│    You      │
└──────┬──────┘
       │
       ├─→ Open Gangway login page
       │   (https://k8s.slac.stanford.edu/<vcluster_name>)
       │
       ├─→ Authenticate with SLAC account
       │
       ├─→ Download kubeconfig + token
       │   (Token expires in ~10 hours)
       │
       ├─→ Run kubectl commands locally
       │
       └─→ Kubernetes API (vcluster)
           │
           └─→ Deploy Pods, Services, Deployments
```

### Current setup: vclusters
Vclusters are a lightweight, virtualized Kubernetes cluster that runs inside a namespace of a parent Kubernetes cluster. They provide a way to create isolated Kubernetes environments for different users or teams without the overhead of managing multiple physical clusters. This allows us to efficiently utilize our resources while providing flexibility and isolation for different workloads and users.



## How do I deploy an application on Kubernetes?

An overview of the deployment workflow:

```
APPLICATION CODE
└─→ docker build → Docker Image

CONTAINER REGISTRY
└─→ docker push → Stored Image (myapp:v1.2.3)

DEPLOYMENT REPO 
└─→ Kustomize manifests reference image

KUBERNETES CLUSTER
└─→ kubectl apply → Pulls image → Runs containers

EXTERNAL ACCESS
└─→ Ingress → Routes traffic to containers
```

1. Ensure you have access to the vcluster you want to deploy your application on (see above).

2. Create a dedicated deployment repo for your application. This repo should contain all the necessary Kubernetes manifests (yaml files) that describe the desired state of your application. 


The deployment repo should follow the structure:

```deployment-repo/
├── kubernetes/
│   ├── overlays/
│   │   ├── (dev or prod)/
│   │   │   (if more than one component, e.g. frontend/backend, can have subdirs here containing manifests specific to that component)/
            - kustomization.yaml
            - deployment.yaml
            - endpoints.yaml 
            - Makefile
```


How the deployment repo manifests map to the Kubernetes stack:

```
External User Request
↓
INGRESS ✓ (endpoints.yaml)
- Handles incoming traffic
- Routes to service based on URL path
- Handle authentication (if needed)
↓
SERVICE ✓ (endpoints.yaml)
- Type: ClusterIP
- Exposes port 8000 internally
- Selects pods with app=iri-mock-s3df
↓
PODS ✓ (deployment.yaml)
- Runs your application container
- Configure replicas, resource limits, environment variables, etc.
```
- endpoints.yaml handles ingress and service definitions
- deployment.yaml handles pod creation/management
- The Makefile:
    - Validates you're on the right cluster before doing anything
    - Generates credentials on-the-fly from stored secrets
    - Deploys via kustomize
    - Cleans up credentials immediately after
    - All in one command: `make apply`


### Why is it structured this way?

The separation of concerns between the application code and the deployment manifests allows for smoother development and deployment workflows.

The deployment repo is structured to follow best practices for Kubernetes deployments, such as using Kustomize for managing application components and resources, and using a Makefile to automate common deployment tasks. This declarative approach allows for easier management of the application lifecycle, including updates and rollbacks, while also providing a clear separation between the application code and the deployment configuration.

