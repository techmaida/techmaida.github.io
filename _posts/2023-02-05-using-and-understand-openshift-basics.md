---
layout: post
title:  "Using and understanding OpenShift - Basics"
date:   2023-02-05 00:00:00
author: "João Paulo Maida"
tags: "DevOps, PaaS, Kubernetes"
comments: true
---

Red Hat OpenShift is DevOps tool, which is acquired or sold as a PaaS, that really puts the customer into a new level. And when I say "a new level" I mean serious because the tool is complete. With one shot you can get all your apps deployed inside containers with all ease that Kubernetes brings.

And, by the way, I forgot to mention. OpenShift is built on the top of Kubernetes, so you can reuse all previous knowledge about Kubernetes, including `kubectl` CLI, architecture and enjoy at the same time a new level of abstraction. This new flavour has the objective to make some operations easier, provide a friendly interface to user and offer the ease to install other Red Hat products, such as AMQ or Red Hat Single Sign On, inside OpenShift [1].

An important question has to be made at this point: has a company unlocked all DevOps and Cloud-Native features just because acquired OpenShift? The answer is pretty simple, no. But understanding this common misunderstanding is not simple and would lead us to a detour in this article. What you need to know now is that OpenShift is able to make things happen faster, and when I say "things" I mean cultural and technological. But in order to achieve the so dreamed DevOps and Cloud-Native status is a long way maturing road.

So, without further due. Let's get into it.

## How to use it?

### Installing

Access `https://developers.redhat.com/products/openshift-local/overview` and click on "Try OpenShift in our free sandbox" button.

![Try OpenShift in our free sandbox](/assets/img/using-and-understanding-openshift-basics/sandbox.jpg)

You'll be request a Red Hat account. If you don't have it, create one.

![Red Hat login](/assets/img/using-and-understanding-openshift-basics/red-hat-login.png)

Click on the button which starts the sandbox (usually is a red button in the top of the page). The following screen will be presented.

![OpenShift login](/assets/img/using-and-understanding-openshift-basics/openshift-login.png)

Use the "DevSandbox" option. You'll be presented to OpenShift homepage. On uppper right corner click in your login name and select "Copy login command". You'll be request again to select "DevSandbox", click on it. A white page will be displayed with a blue hyperlink "Display Token", click on it. Once clicked copy the `oc login` command, paste it into a terminal and hit enter. You are ready to go.

### Basic Concepts

How your applications can run inside an OpenShift cluster ?

That's quite simple. An application exists inside the OpenShift organism as a pod. A pod, which is concept from the Kubernetes world, is the smallest unit possible, can be reflected as a YAML or JSON artifact, and represents an instance of something running. Every entity in the OpenShift or Kubernetes world can be reflected in that fashion. Inside a pod you can have one or multiple containers. That brings an important question. What is the good practice about it? OPOC (One Pod One Container) or OPMC (One Pod Multiple Containers)?

![OPOC x OPMC](/assets/img/using-and-understanding-openshift-basics/opoc-opmc.jpg)

The answer is simple, there is none. It depends on the situation and you must have in mind: if one pod goes down all containers inside follow the same path. That's your compass. You must take your decision based on that.

A pod doesn't live by its own, it lives inside a namespace. A namespace is a logical division to workloads. Understand as a workload any productive applications that can run in a container and, therefore, are pods. You can easily find on internet that there are some default namespaces in OpenShift, and that's not a lie. OpenShift's inside components are also divided in namespaces so you can easily find them and see how they work. A namespace is also important to divide applications in a semantic way inside an enterprise fashion. So, if your company has billing, staff, accounting, sales and others departaments you have a big chance to see that division reflected in namespaces. Usually that's a good approach because it continues the dialect that is spoken in the company.

![Namespace and containers](/assets/img/using-and-understanding-openshift-basics/namespace_and_containers.jpg)

To make the subject here discussed more feasible lets imagine a namespace which concentrates an PHP application and its database.

![PHP application and its database](/assets/img/using-and-understanding-openshift-basics/app-and-database.jpg)

How this application can communicate with the database? I assume that you're thinking about using the IP to directly close de communication, am I right?

![Direct communication via IP](/assets/img/using-and-understanding-openshift-basics/direct-communiction-via-ip.png)

That would work, perhaps, just at the first glance, but in the very moment that any of these pods fails and gets deleted a new is generated, a new IP address is given to that pod. That is an important feature in OpenShift and in the cloud-native world. Pods and consequently must be deleted and regenerated all the time in a fast way, so it's implicit that application must have fast startup and shutdowm times. So, at the end, you cannot use direct communication such as IP addresses or local storage like using the filesystem to store files or memory to data.

But the question remains: how a container can communicate with other in a safe way?

![Application communicates with database via service](/assets/img/using-and-understanding-openshift-basics/comm-via-svc.jpg){:style="display:block; margin-left:auto; margin-right:auto"}

There is an element both present in Kubernetes and OpenShift called Service meant to resolve this issue. A service works like a DNS host, in other words, performs a search by given name and redirects the request to the IPs registered above that name. But how a service would know the correct IPs to redirect to if containers receives new IPs all the time? Each service has a selector, a way to describe which pods it will bind. When a new pod is created there is or not a match and that pod and its IP get into line.

With this approach a consumer, the application in our scenario, doesn't have to concern where the database is. It only points to http://<service-name>.<namespace>.svc.cluster.local:<port>. This URL is just for internal cluster communications.

But ... what if application A tries to send request to application B and B has multiple pods? How that would be handled? The answer is easy. OpenShift/Kubernetes services acts as load balancer. Once you hit the patterned URL showed above, the service will handle the rest, and the load-balancing algorithm can be customized in OpenShift scenarios. So, in a enterprise scenario expect multiple pods and services, it's rare to see an application without service.

Using the same scenario (application + database), how this application would be accessed by client outside the cluster? The routing layer comes to action.

![Routing layer](/assets/img/using-and-understanding-openshift-basics/routing-layer.jpg){:style="display:block; margin-left:auto; margin-right:auto"}

There is an entire routing layer dedicated to address this issue. So, if users or applications that live outside the cluster need to communicate with our application, they both can use this layer to achieve this goal. A route is an exclusive OpenShift object that basically connects itself with a service and expose a URL to external access. Non-secure or secure use cases of the HTTP protocal are addressed in this object.

So, following the breadcrumb trail, a request comes from an external client (user or application) and is received by the route. The route redirects the call to the service and the service acts as a load-balancer redirecting to the pods.

A commom question is: can my application send/receive data using the route even if it's communicating with an application which is deployed inside the cluster? Yes you can but you are overheading the communication because the service already gives you the opportunity to communicate using plain HTTP.

Now you have in your pocket what can be considered the basis related to how OpenShift works and handles applications. But we, as software engineers, know that there is a huge amount of concerns that live around these simples concepts. One of these concerns are: how an application could be updated on OpenShift? In

* Definição do produto
* Como usar
    * Instalação
    * Uso
    * Interface web e CLI
* Conceitos básicos
* Implantando uma aplicação e mais alguns conceitos
    * 2 jeitos
        * new-app direto
        * s2i com build

## References

1. https://www.redhat.com/en/technologies/cloud-computing/openshift