---
title: "Virtual Kubelet"
date: 2017-12-12T10:30:50-06:00
tags: ["Kubernetes", "Microsoft"]
---

Last week was [KubeCon](https://events.linuxfoundation.org/events/kubecon-and-cloudnativecon-north-america). 4,100 Kubernauts descended on Austin, Texas to talk about all things Kubernetes and Cloud Native. During this spectacular event, Microsoft announced a new open-source project called [Virtual Kubelet](https://github.com/virtual-kubelet/virtual-kubelet) that a number of my colleagues (credited below) and I got together a week early in Austin to hack on. I’m super excited about this project, and I’d like to explain a bit about what it is and why it’s so interesting.

### What is the Kubelet?

Before I get into Virtual Kubelet it helps to understand the role that the [Kubelet](https://kubernetes.io/docs/concepts/overview/components/#kubelet) plays in Kubernetes. If you’re already familiar with this, please feel free to skip this section.

First let’s talk a bit about how Kubernetes works from an abstract point of view. Kubernetes serves as a constant reconciliation loop. Desired state is submitted to the [API server](https://kubernetes.io/docs/concepts/overview/components/#kube-apiserver), then controllers and Kubelets and other components within the system constantly work toward achieving this desired state.

![Kubelet](/img/vkubelet/kubelet.png)

Kubernetes has a number of [components](https://kubernetes.io/docs/concepts/overview/components/) within its control plane that serve very specific purposes. The [Kubelet](https://kubernetes.io/docs/concepts/overview/components/#kubelet) is the agent that runs on all nodes to manage pod lifecycle. When the Kubelet launches, it adds itself as a node through the Kubernetes API Server. The [scheduler](https://kubernetes.io/docs/concepts/overview/components/#kube-scheduler) then assigns work to the node by updating the pod resource in the API and assigning a value to the `nodeName` property. The Kubelet watches the [Kubernetes API server](https://kubernetes.io/docs/concepts/overview/components/#kube-apiserver) for any changes to pods that have that `nodeName` assigned. It continuously reconciles the differences by creating new pods as they are scheduled, deleting pods that no longer exist, and updating associated resources like ConfigMaps and Secrets mounted as volumes.

The Kubelet also:

- Calls the configured container runtime (Docker, Rkt, etc) to create, update, delete containers on the host.
- Pulls images from the image registry associated with pods assigned to this node.
- Creates and mounts volumes within a container
- Injects environment variables and updates volumes with Secrets, ConfigMaps, and the Downward API
- Updates the API Server with the latest [Pod](https://kubernetes.io/docs/concepts/workloads/pods/pod/) statuses
- Provides an API for the API Server to call for things like
    - kubectl exec
    - kubectl attach
    - kubectl logs
    - metrics used by the scheduler and dashboard
- Configures Pod networking

Check out this [great post by Jamie Hannaford on GitHub](https://github.com/jamiehannaford/what-happens-when-k8s), if you’d like a more in-depth overview of all the steps of the lifecycle from calling `kubectl` to seeing your pod running.

### What is Virtual Kubelet?
Virtual Kubelet is a project that, from the viewpoint of its interactions with the Kubernetes API, appears to be a Kubelet. The Virtual Kubelet is an application that runs inside a container within your current cluster and masquerades itself as a node. It does this by creating a node resource through the Kubernetes API. It then monitors scheduled Pods the same way an actual Kubelet does. This is the point at which things start to differ. Rather than interact with a host, and with the container runtime on the host, the Virtual Kubelet has modular, embedded backends called providers.

A provider is called by the core Virtual Kubelet logic any time a Pod lifecycle event occurs, to notify the provider it needs to handle a creation, update, deletion, etc of a pod. This allows for numerous possibilities of what a `node` within a Kubernetes cluster can be backed by. The provider itself doesn’t need to worry about injecting ConfigMaps and Secrets, or implementing a reconciliation loop to determine if something needs to be created, updated or deleted. This is all handled by Virtual Kubelet to make implementing providers as seamless as possible.

The first provider we implemented was for [Azure Container Instances](https://aka.ms/T8ul98), also known as ACI. If you’re not familiar with this offering, it’s essentially pods as a service. No need to worry about underlying VMs or control plane management; you only need to worry about your Container Group definition and Azure will handle the rest. You pay per second that your container is running.

![Virtual Kubelet](/img/vkubelet/vkubelet.png)

### What can I use Virtual Kubelet for?
By this point you’re probably thinking, “Ok, Erik, that all sounds interesting, but what is this useful for?” Here is the exciting part: the applications are limitless. Let’s talk about some of the most appealing ones.

- Batch Jobs - You don’t need to have enough VMs running in your cluster to support your batch workloads. You only need to pay for your normal workloads, and batch jobs can fan out as wide as needed to complete them in less time, while you pay per second.
- CI/CD - No need to run additional hardware or VMs that sit idle when you don’t have tasks in your CI/CD pipeline. You only pay per second while tasks are running. Additionally, when you have commit-heavy days, you can avoid a long wait for all of the commits to make it through the queue. They can all be run in parallel without the need to have idle VMs to support the capacity.
- Serverless - Serverless is really starting to catch on, and while the warm-up time of containers isn’t quite as speedy as Azure Functions or Lambda, this does have a lot of appeal. It allows you to leverage the same technologies you’re already using.
- Bursting - This will be very interesting as more support is built out into the Virtual Kubelet to run all workloads. If you use auto-scaling, and your traffic comes in spikes, you only need to run with enough capacity for your average workload; as you run out of capacity in your cluster the scheduler can start placing additional pods in something like ACI or another provider.

Other interesting ideas:

- gRPC - This could call out remotely to a provider implemented as its own application rather than embedded inside the Virtual Kubelet
- VMs - The Virtual Kubelet could be used to provision virtual machines and to run the containers within those virtual machines for complete isolation in multi-tenant environments.
- ??? - I’m really excited to see what other use cases the community comes up with!


### What's next?
This is still a prototype and we’re working hard to pull in more Kubernetes features and talking with many other providers and community members that use container offerings similar to ACI.
I’m really excited to see how this evolves! As always, please feel free to file issues, and PRs are always welcome. The project can be found on GitHub: [https://github.com/virtual-kubelet/virtual-kubelet](https://github.com/virtual-kubelet/virtual-kubelet)

Upcomming features:

- Downward API
- Logs
- Exec / Attach

### The amazing team!
Below is the amazing team of Microsoft developers that made this happen in such a short time. We all came together from various different teams and organizations within the company, and it was such a rewarding experience.

- Brian Ketelsen
- Erik St. Martin
- Jess Frazelle
- Julien Stroheker
- Neil Petersen
- Ria Bhatia
- Rita Zhang
- Robbie Zhang
- Sertac Ozercan