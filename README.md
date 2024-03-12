# kubectl-plugins

## Introduction

A collection of plugins for kubectl integration.

## Installing kubectl plugins

A plugin is a standalone executable file, whose name begins with `kubectl-`. To install a plugin, move its executable file to anywhere on your `PATH`.

### Example

```shell
sudo chmod +x ./kubectl-ssh

sudo mv ./kubectl-ssh /usr/local/bin
```
## Checking for plugin warnings

You can use `kubectl plugin list` command to ensure that your plugin is visible by `kubectl`, and verify that there are no warnings preventing it from being called as a `kubectl` command.

```shell
kubectl plugin list
```

## kubectl ssh

Supports 

1. fast ssh onto kubernetes nodes and 

2. nsenter into any pod's container linux namespace.

> Some dir paths might need revising according to actual situation.

### Usage

Provider-agnostic way of opening a remote shell to a Kubernetes node.

Enables you to access a node even when it doesn't run an SSH server or
when you don't have the required credentials. Also, the way you log in
is always the same, regardless of what provides the Kubernetes cluster
(e.g. Minikube, Kind, Docker Desktop, GKE, AKS, EKS, ...)

You must have cluster-admin rights to use this plugin.

The primary focus of this plugin is to provide access to nodes, but it
also provides a quick way of running a shell inside a pod.

Examples: 
```shell
  # Open a shell to node of a single-node cluster (e.g. Docker Desktop)
  kubectl ssh node

  # Open a shell to node of a multi-node cluster (e.g. GKE)
  kubectl ssh node my-worker-node-1

  # Execute the command ls on a node my-worker-node-1
  kubectl ssh node my-worker-node-1 ls

  # Nsenter into network namespace of a pod
  kubectl ssh pod my-pod

Usage:
  kubectl ssh node [nodeName] [command]
  kubectl ssh pod [podName] [-n namespace] [-c container]
```