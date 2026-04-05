# Kubernetes Assignment 7

This repository contains my implementation of **K8s Assignment 7** using **Minikube**. The lab covers advanced Kubernetes scheduling and pod behavior concepts, including node pinning, node selectors, taints and tolerations, node affinity, QoS classes, DaemonSets, and Static Pods.

## Lab Topics Covered

### 1. Schedule a Pod on a Specific Node Using `nodeName`
Created a Pod named `static-pinned` using the `nginx:latest` image and pinned it directly to the `minikube` node with `spec.nodeName`.

### 2. NodeSelector — Label-based Scheduling
Added the label `env=lab` to the node, created a Pod named `selector-demo` with `nodeSelector`, and verified scheduling behavior. Then removed the label and created `pending-selector` to confirm the Pod remained in `Pending` state.

### 3. Taints and Tolerations
Tested Kubernetes taint effects:
- `NoSchedule`
- `PreferNoSchedule`
- `NoExecute`

Verified that Pods without tolerations were blocked or evicted, and that Pods with matching tolerations were allowed to run.

### 4. Node Affinity — Required vs Preferred
Created Pods using:
- `requiredDuringSchedulingIgnoredDuringExecution`
- `preferredDuringSchedulingIgnoredDuringExecution`

Confirmed that required affinity blocks scheduling when labels are missing, while preferred affinity allows scheduling even if the preferred label is unavailable.

### 5. QoS Classes
Created one Pod for each QoS class:
- `Guaranteed`
- `Burstable`
- `BestEffort`

Verified each Pod’s QoS class using `kubectl describe` and pod status output.

### 6. DaemonSet — One Pod Per Node
Deployed a DaemonSet named `node-monitor` and confirmed that Kubernetes created one Pod per node.

### 7. Static Pod
Created a Static Pod using a manifest file in `/etc/kubernetes/manifests/`, verified that deleting it with `kubectl delete` did not remove it permanently, then removed the manifest file to delete it completely.

## Files Included

- `static-pinned.yaml`
- `selector-demo.yaml`
- `pending-selector.yaml`
- `toleration-pod.yaml`
- `affinity-required.yaml`
- `affinity-preferred.yaml`
- `guaranteed-pod.yaml`
- `burstable-pod.yaml`
- `besteffort-pod.yaml`
- `node-monitor-ds.yaml`
- `k8s_proof.txt`

## Environment

- Kubernetes: Minikube
- Node: `minikube`
- OS: Ubuntu
- CLI Tool: `kubectl`

## Verification

The required command outputs were collected in:

- `k8s_proof.txt`

This file contains proof for the required deliverables in the assignment.

## How to Run

Apply each manifest using:

```bash
kubectl apply -f <file-name>.yaml
