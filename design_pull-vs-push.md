---
projects: ["Node"]
categories: ["Design"]
workstreams: ["ws3", "ws6"]
title: "Design: Pull vs. Push for LCM"
weight: 42
# toc_hide: false
# hide_summary: false
description: >
  Design explanation of Pull versus Push technologies
---

![pull-vs-push-plumbing](/images/design_pull-vs-push_plumbing.jpg)
## What is "good plumbing"?

We take plumbing in our homes and facilities for granted.  When I am search of edge technologies I am looking for "good plumbing" that I can take for granted.

Data Centers and Cloud Service Providers have "good plumbing" that allow customers to focus on application lifecycle management programmatically through APIs for their IaaS.  These luxuries do not exist at that edge and customers are asking Intel for the same experience at the edge.  Many of the CNCF Cloud Native softwares were designed with this infrastructure in mind.  It is important to understand how many CNCF projects do not work well for many edge use cases.  Use cases like utility pole, oil rig, vehicle, delivery robot, self-checkout retail store, patient monitoring, battle field tactical drones/operators, renewable wind farms, autonomous data centers.  Many of these use cases are remote, connected by satellite/5g/4g/3g wireless technology, running off batteries.  If we solve these use cases first, all other use cases closer to the cloud will benefit from the innovation in efficiency and OPEX.

### Edge use cases not typically in Telco or Data Centers:
- Devices are behind firewalls, NATs and proxies and no ports will be open between the central management service and target device
- The IP address of the target device may change over the life of it's deployment
- Devices may be in motion and not stationary
- There is limited physical real estate to have a management hardware near target devices
- Cost and skillset is limited at locations
- Majority of devices do not have a BMC
- Out-of-band Provisioning and In-Band Provisioning will most likely be done in different physical locations
- Massive quantity of devices in different geos
- Generally, there is an army of boots on the ground which require minimal training
- Sometimes diagnosing a device remotely by human is more costly than shipping a unit to replace it
- Device security and software attestation required in varying degrees

![pull-vs-push](/images/design_pull-vs-push.png)

## Pull vs. Push Technologies

### What is a Push Technology?
Technology that requires the collection of target IP addresses and an authentication such as username and password to perform tasks on the target edge node devices.

Example Software:
- Rancher RKE requires a yaml manifest of target IP addresses, SSH Authorized Keys, port 22 to be open and a separate system to perform tasks on a target device.
- Rancher RKE2 requires the process of logging into a target device, which requires an IP address of the device and authorization to execute a command.
- Metal3/Ironic requires a manifest of IP addresses and authorization to the BMC device.
- Airship requires a manifest of IP addresses and authorization
- IOFog
- OpenShift

Pros:
- Works well in data centers
- Ideal for cloud applications
- CNCF Focused and abstracts certain functions

Cons:
- Scales horribly
- Requires separate management infrastructure 
- Requires additional skills and maintenance

### What is a Pull Technology?
Technology where the target device initiates a connection to a known routable IP address or FQDN, to request tasks to perform on itself.

Example Software:
- PXE Boot, the target devices broadcasts a request where to pull the boot process
- EFI HTTPBoot, the target device broadcasts a request where to pull the EFI from what routable IP address or FQDN
- AMT makes an outbound connection to a known routable IP address or FQDN to wait for tasks to be performed
- FDO
- Smart Edge
- Portainer Agent
- Rancher Agent
- Mesh Central
- Rancher Fleet, ArgoCD
- ZeroTier
- ngrok
- Chrome/Firefox Browser
- lots more, I keep a list of these technologies.

Pros:
- Scales extremely well
- Requires very little knowledge
- Supports all uses cases from edge to cloud
- Works well over Satellite
- works well with devices in motion
- works well with multi-shipment provisioning phases
- works well behind firewalls, NATs, Proxies
- works well with IP address changing

Cons:
- TBD

## Typical Lifecycle Management(LCM) Phases of a Device
- Phase 1: LCM of using an out-of-band operation of installing an operating system plus additional software onto target device
- Phase 2: LCM of operating system upgrades, firmware updates, OS services, container runtime, orchestrator software, virtual machine
- Phase 3: LCM of applications on the orchestrator and/or container runtime

**In order to be successful for the edge, ALL of these LCM phases must use Pull Technology for Plumbing**

Note:
- Single node management at scale only requires LCM Phase 1 and 2
- 99% of the customers we work only require single node management but many anticipate "micro cluster" management or LCM Phase 3
- Customers have requested for a single pain of glass for all of these LCM Phases
- Each of these phases are typically performed in different locations and most likely not from the same company

## Is there a solution that tackles this design?
- There is NOT one solution that exists, let's be the first

## Is there a solution that gets us close to this design?
- Yes, there are few solutions that get us close.  Some 80% of the way.

## Apply what we have learned?
| Software | LCM Phase 1 | LCM Phase 2 | LCM Phase 3 |
| ----------- | ----------- | ----------- | ----------- |
| Rancher | No Support | No Support | Pull Model |
| RKE1/2 | No Support | Push Model | No Support |
| Metal3 | Push Model | No Support | No Support |
| Avassa | No Support | Pull Model | No Support |
| Portainer.io | In Development | Pull Model | Pull Model |
| ESP | Pull Model | No Support | No Support |

NOTE: This must be take into context of bare-metal devices at the edge.

# Next to dive into: What scales better REST API (HTTP/S) or PUB/SUB for the Pull Method?
In theory both protocols should scale well, however, in practice REST API (HTTP/S) scales far greater than PUB/SUB because of implementation.  THere are some great white papers on this.
TBD:  Need to find the white paper I am referring too.
