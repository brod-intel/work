---
projects: ["Node"]
categories: ["Design"]
workstreams: ["ws6"]
title: "Design: Autonomous Hyper-converged Clusters"
weight: 42
# toc_hide: false
# hide_summary: false
description: >
  Design explanation of Autonomous Hyper-converged Clusters
---


NOTE: If you haven't already please take the time read the Pull vs Push Design doc which will give some context to this article.

## Background

Container orchestrators such as Kubernetes does excellent job making sure applications are up, running and placed in the correct location.  Cloud service providers do a great job making sure Kubernetes is up and running.  At the edge, what is keeping Kubernetes up and running?  This luxury does not exist at the edge and our customers are asking for the same experience.  Many of the CNCF Cloud Native softwares were designed with this infrastructure in mind. It is important to understand how many CNCF projects do not work well for many edge use case.

In 2017 there was an article that came out stating that to run and maintain 5-node Kubernetes at the edge was $1,000,000 per year in resources. Another article from last year said that a 3-node Kubernetes is rough $572,000 (I have this saved somewhere, need to find it). Kelsey Hightower, one of 3 inventors of Kubernetes said, "Kubernetes was not designed for the edge, people are using it incorrectly".

For many of our edge customers this is a huge barrier to enter the edge market. If Intel wants to be relevant in this market, we need to remove this barrier.  Again 99% of our customers are only working with single node management, Kubernetes is just an idea or something they are playing with in the lab.  

Considering what we have learned from the Pull vs Push model document:
- How do we provide a pull method for the Lifecycle Management of Kubernetes or any other cluster software?
- With zero expertise to managing Kubernetes
- Without a separate management system in the same LAN?
- How we make Kubernetes Control Plane self-heal in the event of a hardware failure without a human intervening?
- How do reduce the cost to manage Kubernetes itself in 1,000s of clusters?
- How do we make it decentralized and function without the need of the central management system connected?

## What is Autonomous Hyper-Converged Clustering technology?

It is the dynamic process of automatically performing the clustering tasks to join or remove systems, as systems bare-metal or virtual, enter or leave gracefully or by failure in the infrastructure.  In other words, when adding a participating Kubernetes node to a non-existent or existent cluster, it will perform the tasks necessary to bootstrap the node into a Manager or Worker or Manage & Worker role, based on the number of nodes and/or hardware, based on a policy in a decentralized manner.

## Introducing Policy-Based Autonomous Clustering for the Edge (PACE)

### What is PACE?
- PACE is a policy driven distributed consensus utilizing a distributed policy for system management in distributed systems without a separate managing control plane
- PACE is complimentary to centralized system management and clustering software such as Kubernetes, Nomad, MariaDB, Oracle, etc.
- PACE allows autonomous system management when centralized management is not practical
  - Limited resources
  - Limited connectivity / availability
  - Autonomy required
- PACE removes the need for a human to perform the tasks of joining clusters together or repairing cluster in the event of a failure
  - It removes the need to use Rancher RKE or Metal3 for example

![pace-difference](/images/design_pace-difference.jpg)
![pace-policy-driven](/images/design_pace-policy-driven.jpg)
![pace-consensus](/images/design_pace-consensus.jpg)

### Use Case Table to show How PACE impacts
System LCM Processes:
- **OS Provisioning:** using an out-of-band operation of installing an operating system plus additional software onto target device
- **Service Provisioning:**  LCM of operating system upgrades, firmware updates, OS services, container runtime, orchestrator software, virtual machine
- **System Management:** Functional operations to maintain the running state of particular service below an orchestrator or cluster software ie. ETCd, MariaDB, Docker Swarm
- **Application Provisioning:** LCM of applications on the orchestrator and/or container runtime

Definitions:
- Push Model type Technologies - examples: Metal3, RKE1/2
- Pull Model type Technologies - examples: PXE, ESP, FDO, Rancher, Portainer, Thingsboard

| Use Cases | OS Provisioning | Service Provisioning | Service Management | LCM Phase 3 |
| ----------- | ----------- | ----------- | ----------- | ----------- |
| Utility Pole | ESP | FDO | PACE | K8s |
| Telco | Push | Push | Human | K8s |
| Telco | Pull | Push | Human | K8s |
| Telco | Pull | Pull | PACE | K8s |


### Use Case

## What does this really mean?
