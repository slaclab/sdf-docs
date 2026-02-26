# Kubernetes
For users of S3DF Kubernetes, the vcluster is the primary interface for deploying and managing applications. For more information around requesting access, or to create a new vcluster, please refer to [service-compute.md](service-compute.md###how-to-request-a-kubernetes-environment).


## A Developer's Guide to K8s in S3DF
This guide provides an overview of the Kubernetes deployment workflow and best practices for developers working within the S3DF environment. It covers the steps from application code to deployment on a Kubernetes cluster, including how to structure your deployment repository, manage secrets, and automate deployments using Makefiles. 



### Application Deployment Methodology


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

Using GNU Make is a way of "normalizing" the various sources for provisioning K8s resources. For example, a Kubernetes workload could have the following components provisioned from different sources:

- **[HashiCorp Vault](https://www.vaultproject.io/):** A secrets management tool used to securely store and dynamically generate credentials (e.g., database passwords, API keys). The Makefile can retrieve these secrets at deploy time without embedding them in the repo.
- **CRDs for [CNPG](https://cloudnative-pg.io/) (CloudNativePG) from GitHub:** Custom Resource Definitions for the CloudNativePG Postgres operator, fetched directly from its GitHub releases. These extend the Kubernetes API to manage PostgreSQL clusters as native Kubernetes objects.
- **CRs from [Helm](https://helm.sh/) charts:** Custom Resources instantiated via Helm chart deployments. Helm acts as a package manager, rendering and applying Kubernetes manifests (including CRs) from versioned, reusable chart templates.


A Makefile target can be structured to provision and apply the above resources in a Kubernetes deployment with a single command (e.g., `make apply`). This approach also helps to ensure that best practices for security and deployment are consistently followed across all applications deployed in S3DF Kubernetes. 


#### Why is it structured this way?

The separation of concerns between the application code and the deployment manifests allows for smoother development and deployment workflows.

The deployment repo is structured to follow best practices for Kubernetes deployments, such as using Kustomize for managing application components and resources, and using a Makefile to automate common deployment tasks. This declarative approach allows for easier management of the application lifecycle, including updates and rollbacks, while also providing a clear separation between the application code and the deployment configuration.

Similar to `Kubernetes` role as runtime platform for containerized applications, `Helm` serves as a package management and templating layer on top of Kubernetes deployments. Its purpose would be to reduce manifests duplication and enforce consistent policy defaults (security context, read-only mounts, ingress annotations) across your applications deployed in S3DF Kubernetes. Helm allows you to templatize your Kubernetes manifests and manage them as reusable charts, which can be easily shared and versioned. This can help streamline the deployment process and ensure that best practices are consistently applied across all your deployments.
