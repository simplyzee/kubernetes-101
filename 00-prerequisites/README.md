# Before you start

You need to make sure you have a suitable development environment. You have a couple of choices here:

* Install everything locally using Kind
* Spin up an AWS EKS Cluster

## Install the AWS CLI

Ignore this step if you already have the AWS CLI.

Install using homebrew:

``` bash
brew install awscli
```

## Install Kubernetes Client Binary

You will need to install `kubectl` to interact with the Kubernetes API.

``` bash
brew install kubernetes-cli
```

## Install Kubernetes Locally

If you've chosen to run Kubernetes locally then you will need `kind` to spin up a lightweight Kubernetes cluster

``` bash
brew install kind
```
