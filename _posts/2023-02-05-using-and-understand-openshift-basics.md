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