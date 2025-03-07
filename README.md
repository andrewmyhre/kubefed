[![Build Status](https://travis-ci.org/kubernetes-sigs/kubefed.svg?branch=master)](https://travis-ci.org/kubernetes-sigs/kubefed "Travis")
[![Go Report Card](https://goreportcard.com/badge/github.com/kubernetes-sigs/kubefed)](https://goreportcard.com/report/github.com/kubernetes-sigs/kubefed)
[![Image Repository on Quay](https://quay.io/repository/kubernetes-multicluster/kubefed/status "Image Repository on Quay")](https://quay.io/repository/kubernetes-multicluster/kubefed)
[![LICENSE](https://img.shields.io/badge/license-apache2.0-green.svg)](https://github.com/kubernetes-sigs/kubefed/blob/master/LICENSE)
[![Releases](https://img.shields.io/github/release/kubernetes-sigs/kubefed/all.svg)](https://github.com/kubernetes-sigs/kubefed/releases "KubeFed latest release")

# Kubernetes Cluster Federation

Kubernetes Cluster Federation (KubeFed for short) allows you to coordinate the
configuration of multiple Kubernetes clusters from a single set of APIs in a
hosting cluster. KubeFed aims to provide mechanisms for expressing which
clusters should have their configuration managed and what that configuration
should be. The mechanisms that KubeFed provides are intentionally low-level, and
intended to be foundational for more complex multicluster use cases such as
deploying multi-geo applications and disaster recovery.

KubeFed is currently **alpha** and moving rapidly toward its initial
[beta release](https://github.com/kubernetes-sigs/kubefed/milestone/4).

## Concepts

<p align="center"><img src="docs/images/concepts.png" width="711"></p>

KubeFed is configured with two types of information:

- **Type configuration** declares which API types KubeFed should handle
- **Cluster configuration** declares which clusters KubeFed should target

**Propagation** refers to the mechanism that distributes resources to federated
clusters.

Type configuration has three fundamental concepts:

- **Templates** define the representation of a resource common across clusters
- **Placement** defines which clusters the resource is intended to appear in
- **Overrides** define per-cluster field-level variation to apply to the template

These three abstractions provide a concise representation of a resource intended
to appear in multiple clusters. They encode the minimum information required for
**propagation** and are well-suited to serve as the glue between any given
propagation mechanism and higher-order behaviors like policy-based placement and
dynamic scheduling.

These fundamental concepts provide building blocks that can be used by
higher-level APIs:

- **Status** collects the status of resources distributed by KubeFed across all federated clusters
- **Policy** determines which subset of clusters a resource is allowed to be distributed to
- **Scheduling** refers to a decision-making capability that can decide how 
  workloads should be spread across different clusters similar to how a human
  operator would

## Features

| Feature | Maturity | Feature Gate | Default |
|---------|----------|--------------|---------|
| [Push propagation of arbitrary types to remote clusters](https://github.com/kubernetes-sigs/kubefed/blob/master/docs/userguide.md#example) | Alpha | PushReconciler | true |
| [CLI utility (`kubefedctl`)](https://github.com/kubernetes-sigs/kubefed/blob/master/docs/userguide.md#operations) | Alpha | | |
| [Generate KubeFed APIs without writing code](https://github.com/kubernetes-sigs/kubefed/blob/master/docs/userguide.md#enabling-federation-of-an-api-type) | Alpha | | |
| [Multicluster Service DNS via `external-dns`](https://github.com/kubernetes-sigs/kubefed/blob/master/docs/servicedns-with-externaldns.md) | Alpha | CrossClusterServiceDiscovery | true |
| [Multicluster Ingress DNS via `external-dns`](https://github.com/kubernetes-sigs/kubefed/blob/master/docs/ingressdns-with-externaldns.md) | Alpha | FederatedIngress | true |
| [Replica Scheduling Preferences](https://github.com/kubernetes-sigs/kubefed/blob/master/docs/userguide.md#replicaschedulingpreference) | Alpha | SchedulerPreferences | true |

## Guides

### User Guide

Take a look at our [user guide](docs/userguide.md) if you are interested in
using KubeFed.

### Development Guide

Take a look at our [development guide](docs/development.md) if you are
interested in contributing.

## Code of Conduct

Participation in the Kubernetes community is governed by the
[Kubernetes Code of Conduct](./code-of-conduct.md).
