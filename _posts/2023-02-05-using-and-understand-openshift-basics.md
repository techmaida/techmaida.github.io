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

## "Installing"

Access `https://developers.redhat.com/products/openshift-local/overview` and click on "Try OpenShift in our free sandbox" button.

![Try OpenShift in our free sandbox](/assets/img/using-and-understanding-openshift-basics/sandbox.jpg)

You'll be request a Red Hat account. If you don't have it, create one.

![Red Hat login](/assets/img/using-and-understanding-openshift-basics/red-hat-login.png)

Click on the button which starts the sandbox (usually is a red button in the top of the page). The following screen will be presented.

![OpenShift login](/assets/img/using-and-understanding-openshift-basics/openshift-login.png)

Use the "DevSandbox" option. You'll be presented to OpenShift homepage. On uppper right corner click in your login name and select "Copy login command". You'll be request again to select "DevSandbox", click on it. A white page will be displayed with a blue hyperlink "Display Token", click on it. Once clicked copy the `oc login` command, paste it into a terminal and hit enter. You are ready to go.

## Basic Concepts

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

A commom question is: can my application send/receive data using the route even if it's communicating with an application which is deployed inside the cluster? Yes you can but you are overheading the communication because the service layer already gives you the opportunity to communicate using plain HTTP.

Now you have in your pocket what can be considered the basis related to how OpenShift works and handles applications. But we, as software engineers, know that there is a huge amount of concerns that live around these simples concepts. One of these concerns are: how an application could be updated on OpenShift? In our example the application PHP had some improvements and new version must be deployed. How that would be addressed using OpenShift?

A Deployment is a Kubernetes object widely used and adopted in OpenShift 4 to hold deployment configurations. A deployment holds the template of the future pods, so in this scenario a pod brings the configurations defined in the deployment. And what configurations would be? The used image, environment variables, name, labels, volumes and probes are just a few of what can be find there. Based on all that a pod can be created.

Is always necessary in order to create a pod create a deployment? No.

You can create pods by writing its definition (YAML or JSON) by yourself. The use of a deployment is to make all easier. If a pod gets deleted, using deployment, a new one is created automatically because every deployment works along with a Replica Set. The Replica Set is the object responsible to guarantee that the amount of replicas configured in one deployment will actually exist. This object is created automatically by OpenShift when a deployment is created and application's rollout is done. So our study scenario can be described as the image below.

![Pods + deployment + replica set + inner/outer communication](/assets/img/using-and-understanding-openshift-basics/full-comm.jpg){:style="display:block; margin-left:auto; margin-right:auto"}

One thing is important to consider. According to the third factor [3] in the 12 Factor-App methodology [2] configurations should be both consumed and stored as environment variables. So, to address this concern there are two objects in the Kubernetes/OpenShift world, the Config Map and the Secret. They are like cousins and usually walk together but with one difference. Secrets encode (base64) their data because are meant to sensitive data and Config Maps handle ordinary configuration data.

So, using our scenario to explore these new objects we would have.

![Injecting configuration as environment variables using ConfigMaps and Secrets](/assets/img/using-and-understanding-openshift-basics/injecting-configs.jpg){:style="display:block; margin-left:auto; margin-right:auto"}

In both ConfigMaps and Secrets data can be stored as key-value pairs or as files. Using key-value pairs data will be mounted as environment variables in a deployment and therefore in pod(s). Using as files data will be introduced in configmaps or secrets using key-value pair mode but the key will be the file's name and value its content. OpenShift can notice the difference and mount the data as file using a determined path. Use reference [4] for more details if you're interested.

![Ways to store data in configmaps and secrets](/assets/img/using-and-understanding-openshift-basics/key-value.jpg){:style="display:block; margin-left:auto; margin-right:auto"}

That ends what you need to know about the basics in Kubernetes/OpenShift.

## Deploying your first application

So far we understood all the basics concepts in Kubernetes/OpenShift we're ready to deploy our very first application. You can find several examples on the internet how to do that but just in a few you'll understand how the process works behind the curtains.

One of toppest features on OpenShift is the S2I process. The S2I process can be comprehended by the source code transformation into container image. Of course there is no black magic related to this and details about the process you can find in the docs [5]. But in a nutshell, OpenShift can detect the application runtime (Java, PHP, .Net, Golang, etc) using some verification such as finding an index.php or a pom.xml file, based on that selects the best base image present in the Red Hat Catalog and finally builds an optimized image.

That opens a good discussion about containerization strategies because S2I goes in the opposite direction when compared to Dockerfiles/Containerfiles. It's possible to perform S2I even when there is a Dockerfile but the S2I process eliminates the need of a Dockerfile. So, what's the best?

There is no accurate answer to that. You'll have to decide what is the best approach. One simple rule that I follow is: if your application is just some simple application that has no special requirements such as OS packages or sidecars go with the S2I. But if your case is the opposite, use Dockerfiles.

Let's do some coding now !!! 

We'll use a sample application written in Quarkus to show how easy is to deploy an application on OpenShift. The first thing to have in mind is that you must be logged in OpenShift. If you've done the "Installing" section you'll have no problem.

Using the free sandbox as showed above a namespace is already created. We'll use that. Execute on a terminal the following instructions.
```
oc import-image ubi8/openjdk-11:latest --from=registry.access.redhat.com/ubi8/openjdk-11:latest --confirm -n <namespace>
oc new-app openjdk-11~https://github.com/jpmaida/todo-list-quarkus#quarkus-2.0.0.Final-relational-db -n <namespace>
```

What just happened ?

explicar comandos

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
2. https://12factor.net/
3. https://12factor.net/config
4. https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-configmap/
5. https://docs.openshift.com/container-platform/4.8/openshift_images/using_images/using-s21-images.html