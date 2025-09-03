# S3DF Compute Clusters Overview
The S3DF environment consists of several compute clusters designed to support a variety of computational needs. Below is a detailed breakdown of the different types of nodes and their specific characteristics.

## Node Types
- Login/OnDemand Nodes

  - Purpose: Access to other resources within the S3DF environment.

- Data Transfer Nodes

  - Purpose: Facilitates the downloading and uploading of files.

- Interactive Pool Nodes

  - Purpose: Used for compiling code, submitting jobs, and executing tasks interactively.

- Compute/Batch Nodes

  - Purpose: Dedicated to running High-Performance Computing (HPC) jobs utilizing either CPUs or GPUs.
 
     ![Node types](nodetype.png)

## Compute Node Clusters
The compute nodes are partitioned into three distinct clusters:

### 1. Milano Cluster
- Number of Nodes: 120
- Node Type: Dual-CPU Node
- Memory: 512 GB
- CPUs:
  - 2x AMD Milan 7713 (64 cores each)

### 2. Roma Cluster
 - Number of Nodes: 39
 - Node Type: Dual-CPU Node
 - Memory: 512 GB
 - CPUs:
   - 2x AMD Rome 7702 (64 cores each)

### 3. Ampere Cluster
 - Number of Nodes: 23
 - Node Type: CPU/GPU Hybrid Node
 - Memory: 1024 GB
 - CPUs:
   - AMD Rome 7542 (64 cores)
 - GPUs:
   - 4x Nvidia Tesla A100

This structure of clusters and node types ensures that S3DF can meet a wide range of computational demands efficiently. Please refer to additional documentation for specific usage guidelines and best practices for optimizing performance in your computational tasks.
