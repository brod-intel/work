---
projects: ["Node"]
categories: ["Workflow"]
workstreams: ["ws3", "ws6"]
title: "Design: Pull vs. Push for LCM"
weight: 42
# toc_hide: false
# hide_summary: false
description: >
  Workflows covering the off boarding of bare metal nodes.
---


Data center and cloud environment provide abstraction and obscurity from what is really going below their APis.   Physical systems are racked and stationary and live their lives process data unchanged.  Typical idea of building a management network, front network and backend network, expecting everything to be on a flat network in a trusted lan.  Being able to stand up and tare down virtual networks and virtual machines at will.  Querying a database of IP addresses of the compute within a network.  Many of the CNCF Cloud Native softwares were designed with this infrastructure in mind.  This same luxury does not exist in the edge world.  

Use cases like utility pole, oil rig, vehicle, delivery robot, self-checkout retail store, patient monitoring, battle field tactical drones/operators, renewable wind farm.  Many of these use cases are remote, connected by satellite/5g/4g/3g wireless technology, running off batteries.  If we solve these use cases first, the usa cases closer to the data center will benefit as it will reduce the OPEX.

When evaluating software for particular function we need to put ourselves in the shoes of the installer

## Pull vs. Push Technologies

## What is push tech?
Technology that requires you to gather target IP addresses 


### What scales well?
Client Broswers connecting to CDNs 
