---
slug: step1
id: jg5dplj5k0ev
type: challenge
title: Creating a New Project
notes:
- type: text
  contents: |
    ## Why an Operator?

    Operators make it easy to manage complex stateful applications on top of Kubernetes. However writing an Operator today can be difficult because of challenges such as using low level APIs, writing boilerplate, and a lack of modularity which leads to duplication.

    ## What is the Operator SDK?

    The Operator SDK is a framework that uses the controller-runtime library to make writing Operators easier by providing:

    * High level APIs and abstractions to write the operational logic more intuitively.
    * Tools for scaffolding and code generation to bootstrap a new project fast.
    * Extensions to cover common Operator use cases.

    ## How do I use it?

    The following is the workflow for a new **Go-based** Operator with the Operator SDK:

    1. Create a new Operator project using the SDK CLI.
    2. Create a new Custom Resource Definition API Type using the SDK CLI.
    3. Add your Custom Resource Definition (CRD) to your live Kubernetes cluster.
    4. Define your Custom Resource Spec and Status.
    5. Create a new Controller for your Custom Resource Definition API.
    6. Write the reconciling logic for your Controller.
    7. Run the Operator locally to test your code against your live Kubernetes cluster.
    8. Add your Custom Resource (CR) to your live Kubernetes cluster and watch your Operator in action!
    9. After you are satisifed with your work, run some Makefile commands to build and generate the Operator Deployment manifests.
    10. Optionally add additional APIs and Controllers using the SDK CLI.

    ## PodSet Operator

    In this tutorial, we will create an Operator called a PodSet. A PodSet is a simple Controller/Operator that manages pods.

    A user provides a number of pods specified in `spec.replicas`. The PodSet also conveniently outputs the name of all Pods currently controlled by the PodSet in the `status.PodNames` field.

    Let's begin!
tabs:
- title: Terminal 1
  type: terminal
  hostname: container
- title: Terminal 2
  type: terminal
  hostname: container
- title: Visual Editor
  type: code
  hostname: container
  path: /root
- title: Web Console
  type: website
  url: https://console-openshift-console.crc-dzk9v-master-0.crc.${_SANDBOX_ID}.instruqt.io
  new_window: true
difficulty: basic
timelimit: 500
---
Let's begin by connecting to OpenShift:

```
oc login -u admin -p admin https://api.crc.testing:6443 --insecure-skip-tls-verify=true
```

Now let's create a new project where to work with:

```
oc new-project myproject
```

Let's now create a new directory for our project:

```
mkdir -p $HOME/projects/podset-operator
```

Navigate to the directory:

```
cd $HOME/projects/podset-operator
```

A new Go-based Operator SDK project for the PodSet Operator has been already initialized for convenience with the following command
 `operator-sdk init --domain=example.com --repo=github.com/redhat/podset-operator `

You can list all file generated with this command:

```
ls -lh
```

