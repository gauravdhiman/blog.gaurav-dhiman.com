---
title: Recipe to build large scale web apps
date: 2020-03-21T00:00:00-07:00
keywords:
- web-application
- deployment
- virtualization
- containers
- container orchestration
- serverless
- FaaS
categories:
- Technology
- Architecture
tags:
- scalability
- deployments
- web apps
- microservices
- containers
- Docker
- Kuberneties
- serverless
- FaaS
clearReading: false
coverImage: https://images.unsplash.com/photo-1586772002130-b0f3daa6288b?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1000&q=60
thumbnailImage: https://images.unsplash.com/photo-1586772002130-b0f3daa6288b?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1000&q=200
thumbnailImagePosition: bottom
autoThumbnailImage: true
metaAlignment: center
coverSize: full
comments: true
showTags: true
showPagination: true
showSocial: true
showDate: true
showTOCOnSide: true
disqusIdentifier: recipe-to-build-large-scale-web-apps

---
Today web apps are developed considering global user-base, so they need to scale fast without disruption, to serve global traffic. This post explores the architectural as well as infrastructural needs to scale any web app.
<!--more-->

## Brief history of web apps

Anyone who has worked in software development since last decade or so must have observed a drastic change in the way software is being built today. In early days of Internet, we had more of static websites and gradually taken over by what we used to call as dynamic websites backed up by a database. There was no concept of Web API’s, in memory databases or its likes, just a plain HTML website. In my view, the first real what I would call a dynamic website was a search engine or an online directory (yellow pages). Search engine would accept few keywords and return results at the click of a button. We had qualified a Search Engine as a more of a dynamic web app as it had some kind of logic sitting behind with a user interface at the front accessed via a browser. From that era of heavy backend logic apps, we are here where a significant amount of intelligent App logic is implemented on a front-end supported by majority of the frameworks / libraries in the present times along with backend - think of admin dashboards, web based e-mail clients, front-end of social network  -  all of these involve a lot of User Interface elements, several user interactions and UI changes as a result of those interactions. All this evolutionary phase for web development was so profound that it has almost replaced the need to have a Desktop enterprise Apps. Things are evolved so fast that now even web apps are being outdated by the new world of [Hybrid Apps](https://ionicframework.com/resources/articles/what-is-hybrid-app-development) and PWAs ([Progressive Web Apps](https://developers.google.com/web/ilt/pwa)).

## Problem & solution of scaling-up

Systems that are {{< hl-text cyan >}}rigid{{< /hl-text >}} (complex and tightly coupled components), {{< hl-text cyan >}}monolithic{{< /hl-text >}} (all in one) and are built with {{< hl-text cyan >}}no clear demarcation of functional components{{< /hl-text >}} fail to scale up. In general, to scale up any system,  we need to build a system that is {{< hl-text cyan >}}modular{{< /hl-text >}} (think of plug-n-play components), {{< hl-text cyan >}}loosely coupled{{< /hl-text >}} and {{< hl-text cyan >}}flexible{{< /hl-text>}} (react to changes). This principal is not specific to software systems, but to all kind of systems - think of factories, airports, hospitals, government / political systems. The more you observe how real world systems work, the better system designer you can be and software system design is not in anyway different from it.

To scale up software systems, we need to think of components from two different perspectives {{< hl-text cyan >}}architectural{{< /hl-text >}} and {{< hl-text cyan >}}deployment infrastructure{{< /hl-text >}} perspectives. Let's cover each of these in detail.

### Architectural considerations

Architecturally scale-able applications should have smaller, reusable and independent components that are loosely couples (free to move around in larger system design). Think of how small Lego pieces of different shapes and colors are used to build something big and meaningful. Same way software systems should be build with small components that have plug-n-play interfaces.

{{< image classes="fig-100 center clear" src="https://images.unsplash.com/photo-1568617934289-df4399f8cea3" group="group:travel" title="Photo by Dan Burton on Unsplash" >}}

Any web app can be logically divided into mainly three tiers - Front-end (UI/browser), Middleware (app server) and Database server. Earlier Middleware server layer used to be monolithic (all app logic as single deployable unit). To scale the traditional web app, we used to deploy multiple instances of whole monolithic app either on physical or virtual machines. This was not optimal and great way to scale. This was traditional way of building app ([monolithic architecture](https://www.youtube.com/watch?v=MPpU8y3ykS4)). To explain it better, think of an app having few services - **Authentication**, **User**, **Product**, **Order** etc. In a monolithic architecture, single deployable unit will have whole app (middleware server), including all the services. If another instance is needed, , the entire app needs to be deployed (monolithic way). Single unit of deployment in monolithic app looks like below.

{{< image classes="fig-100 center clear" src="https://lh3.googleusercontent.com/_Jtqzvnp3ELXaUxpDhzDffdMhX-WmpWkz20UsJ1_QEmR7DaHwS3ew_ZuBlYho4b1MzY6lO7gkDpf0Qvvw0RS5iOSRtDLupRKojXgOK4_i2Mh9VQwiUvRUG8Vc5cJWjxNAFj9Bq2hBnm5HVBIxlgD13Bjg4UoKHvclAEZ0Vdfipxtn_LVE5y6B7mS2u5bxGYpg_zKQOsql2blsSH27uDgjx2212MRvbzjUtYWjYNg2KaLfPk6Ghn1Nt3LSKzvxZq5RTkV0G9t9iJu6gJjLMBGpAg7YYgVv98j1J6JreRVX0wGqSP0JDNRw0USivTPpo-ZsYYgdyIi5QqHyrA9OuDJkSa1ShMn00k_AzhX7Gewc7hvXCrgbbWLKxC1nO2XfNjvPN3135DSJTdFGxAwU7GsZFMlt3h8m-ZFdGbo6IUhPLSto8v8oK9OWllJB7tujkUpWwuNKpabJHU7dNUNtNIwtSb7k9gTPCbyH7V4iT60_F_mjnm7obQsuV5oAtfY-h46PsvpYRskYrniymi9afz5SNTte4ic-ZU4B3zf1QnmR9osi7ooSwhKWkpeKwDLHlGdNV7Ig--J3Mmx0tJc1U9Z0g7Pkdt8_67QAiXjPhHqJ2ckx9hrpK5q-CTcqPvJDCcPfwsZMOIhJDIDdHBJ6B6ixQ-YY8BccWLPBjn-UrswVJRTZH6u3rFLgNk92WBX7Q=w2290-h1327-no" group="group:travel" title="Monolithic Architecture" >}}

If one or more services are used more in application as compared to others, then why we need to deploy less used services with each deployment (app instance) - no point of scaling the service which is hardly or less used. We need to scale up the components of app that are more used (get more web traffic). For instance, {{< hl-text cyan >}}Order service{{< /hl-text >}} would not be as heavily loaded as {{< hl-text cyan >}}Product service{{< /hl-text >}}. Order service will be used only by logged in users who wants to buy a product, where as the product service will be used by both logged-in and non-logged-in users to view the product details on product page. With this understanding, we should have made each service as independent and loosely couple unit of deployment. This is known as [microservices architecture](https://docs.microsoft.com/en-us/azure/architecture/guide/architecture-styles/microservices), where each service (logical unit of business function) is a independently deployable unit. Below diagram shows the same.

{{< image classes="fig-100 center clear" src="https://lh3.googleusercontent.com/4mHRQGQWOW_itf2L0vu_CSBVjGOfjCGvNJZucokkZdBAfugUFgWH9BZR3ZG1webchGSNo7l5EpPLCcSMWmo_YGUP5MstvvcTV138Dke2JHMUfatg8Sg_h6LNnTHBb-YOaEmsnYnOoPcPGEK1ErU4mnTenH-_yWlXImuw3-PsrlKFtG-ihY1ajuTp3G_BPKZJvYl8lePdR6mCXxBecffAFZ4do7D4meJgdwnzGK_nFRYHodnYmdTz1ufwx5nn7xOOFSCqEH-_8eJoSU_opXqDw4-IXLoQtgLQAF7C8p1VAmJ9iue2h7eVSfnKzHs0Ds6IZdzbKHoCfZSbU74bBLio7iDC_wKgYCaXn7ARuYjNkdVMxlSsVNVLEpMfEzG50xqx8igUWHpORE-mzjK5O91rOV39LPW45Jfxms-W1mc0Ow_K__r06B9udCC3rjH8aH8YqJdeMbsROPWiLBSxNXWEhyCi1nCKM8Jhmm4gEAltZ6vSjlfuiChGw7R6m3eTuBQG-Z4Ibca3tgPmIoxj2kiyC4ZipoTMiyOOSzt_K7k-ysJc8fvWGe9UBwLm7NGHG7r1UlQVfcWMDL6a0sT7_7enY8c6VPLuwJxjPoSdKgzRfMlmeERRinuiBfK447nLK8q_P3jMRg0PrEUDzscWHCxUcUS-DuIuuAWcAfi1JIY1wcFHlKUo95ZO1hyf0TV5jg=w1837-h1802-no" group="group:travel" title="Monolithic Architecture" >}}

Below diagram sums-up the difference between a monolithic and microservices architecture. Here you can see, in monolithic architecture everything is packaged in every single instance of deployment, whereas in Micoservices based architecture, the application is broken down into small functional units (called microservices) and each of those can be deployed separately based on needs for  scaling up.

{{< image classes="fig-100 center clear" src="https://dannyvanderkraan.files.wordpress.com/2017/02/serverless-on-azure-figure-5-2.png" group="group:travel" title="Monolithic vs Microservices Architecture" >}}

Same as Middleware (server app), a Database layer also can be scaled up/down. To make database scale-able, it needs to be running on cluster of nodes, all nodes being configured as active-active with data getting spread?? over all nodes. Cluster management involves scaling up the cluster size by including new nodes in the cluster without any downtime. Generally, while architecting a scale-able app, a distributed database is chosen and run in active-active cluster.

### Deployment infrastructure considerations

Along with application architecture, the underlining infrastructure plays a huge role in making the app truly scale-able. Even the well designed, microservices based web app can not scale if the underlining deployment infrastructure is not scale-able. In this section I will talk more about deployment strategy. Technology and tools for deployment and managing infra has changed drastically in last few years, mainly in last 15 years. Below diagram shows the snapshot of change from traditional way of deployment on physical servers to virtualized deployments to containerized deployments.

{{< image classes="fig-100 center clear" src="https://www.scaleway.com/assets/images/docs/kube-intro/Deployment_Evo.png" group="group:travel" title="Changes in deployment approach over years. (Image credit: www.scaleway.com)" >}}

#### Deployment on physical server environment

Web applications were primarily deployed on a physical infrastructure (aka blade servers). Managing and scaling such an Infrastructure involved huge upfront investment and a immense manual work. On top of it, scaling it wasn’t easy and if was feasible it used to come with additional humongous cost.. Needless to mention that it required a lot of planning in advance, very often delayed implementations and leading to loss of opportunities for businesses. Scaling the infrastructure on demand was not possible. Below diagram shows the traditional deployment model where an application is deployed on physical infrastructure.

{{< image classes="fig-100 center clear" src="https://lh3.googleusercontent.com/o2c1WKWjH_OasaADJ4OHTk45FvDyDcL0qXKqN_Z8arl1rJkv4dSP0wv2YA90n8ct_fozsGfajCg_SzKGMfw2jazlDYEteHZzKNYjg2m014I3Qym9sUDsDz29hX2S2iZkLvChzuMYBrSbTkM_0sgBkUPTIJ2E6KwjJ7Ba-zbakxLnej8b2PAFVi6hk0Rbb5mx30DuhpjYCktEcnC_K9vsNPtMZxwxt00yq-Vvc3C99Q1cSzL_uiq-dnLssMWAxqiDWrlfdv5wpE0seXRzAEcY5PAhafM8k8sbO3SL_MYdmwKhIGGRvyZe9Cvj6QNTIgIw641KIe8Kahlia9H9S-Pjn5oJkup3EiMf_TkbvadeO2pCCE6mEonXD-HRvg39aJVNytdOGwMjvMSFgSQ0GGaJr9biCTGeCh16qW_Zdw5T8rCmdDL0wPyRGKHBI8VN-K93coM_4rXPWKXDHL-hWBoZtxmiEMDbrJ11fD0dl7siAkOLDNIaKfIxveAYqDROSXvZHyMVV0b02tVj0tAaRj_c6dwrzW6-jbmk8h4TsfjVDyA7N0ZQeCsnIxAauo9WgfctM-scjt49_jt8EXLdqAKjnWKozS0qWihV1NlnIojTD2jk4O38dDRzzTfE5jL196kHQIBLTUyBmQTO1H7BewNCSs8p6ybXmg4J8wt8UHW5r3NN2-UHZst2rbHko-sU_A=w1837-h1570-no" group="group:travel" title="Physical servers cluster." >}}

#### Deployment on virtualized environment

Then came the era of VMs (Virtual Machines). Some of the key advantages of virtualizing the infrastructure was better resource utilization and on-demand scaling. One Physical machine can now host multiple virtual machines (VM) based on the resource requirements for a VM. Multiple VM’s can spun up based on the needs resulting in optimum utilization of the infrastructure. As the demand for resources grow, the underlying VMs management software spins up VMs as required or defined in its configuration, hosting the app instance and bring them up on network almost instantaneously. From the network topology stand-point, virtualized deployment schema looks similar to physical deployment schema, except that physical machine can now host multiple virtual machines. Below diagram is a depiction of how multiple VMs are hosted on single physical machine.

{{< image classes="fig-100 center clear" src="https://miro.medium.com/max/2396/1*oF6QqYRhWPw9HF20CUqhMw.png" group="group:travel" title="Multiple VMs on same PM. (Image credit: www.medium.com)" >}}

#### Containerized deployment

Virtualizing the infrastructure was one step forward in bringing efficiencies but they are still resource intensive when compared with Containers. In this section, I will talk about Containers. Talking about VMs – they require space and memory for Guest OS, common utilities in addition to web app and its dependent packages. Containerization has given us even better ways of bringing efficiencies in our infrastructure. In layman terms, a [Container](https://www.youtube.com/watch?v=0qotVMX-J5s) is packaging of app along with its dependent packages / libraries, without any overload of guest OS and other low level stack. You can think of a container as a light-weight VM, that boots fast and make the app instance available in a matter of seconds. Below diagram depicts multiple Containers hosted on a single physical machine. [Docker](https://docs.docker.com/get-started/overview/) is an example of one of the most popular containerization software that helps manage life-cycle of a container.

{{< image classes="fig-100 center clear" src="https://www.docker.com/sites/default/files/d8/styles/large/public/2018-11/container-what-is-container.png?itok=vle7kjDj" group="group:travel" title="Containers. (Image credit: www.docker.com)" >}}

To manage multiple containers and ensure that they scale up and down as and when required, another cluster aware software is used - in general term that is known as [container orchestration](https://www.youtube.com/watch?v=kBF6Bvth0zw) software. [Kubernetes](https://www.youtube.com/watch?v=PH-2FfFD2PU) is one of the popular container orchestration cluster management software. It ensure that the given cluster configuration is always maintained in run time. Below diagram shows high-level architecture of Kubernetes and how it manages the pods (run time container image) using Docker. In the below diagram, {{< hl-text cyan >}}Node{{< /hl-text >}} represents a single physical or virtual machine. Master node is a management / admin node in cluster and worker nodes / machines are compute nodes (hosts for pods), each one having a container management software (Docker in this case) installed on it. Docker on each worker node is responsible to manage the life-cycle of containers on that node. Kubernetes talk to Docker through {{< hl-text cyan >}}kubelet{{< /hl-text >}} (you can think of them as agent components). They relay commands from API server to Docker on given node. In case you want to learn more about containers and container orchestration and how they compliment each other, watch this short [video about Dockers and Kubernities](https://www.youtube.com/watch?v=2vMEQ5zs1ko).

{{< image classes="fig-100 center clear" src="https://res.cloudinary.com/dukp6c7f7/image/upload/f_auto,fl_lossy,q_auto/s3-ghost/2016/06/o7leok.png" group="group:travel" title="Kubernities Architecture. (Image credit: www.docker.com)" >}}

After going through all of the above, we can easily see how the deployment infrastructure has changed over period and how reactive and scale-able the deployment infrastructure has become, leveraging the cluster capabilities.

#### Serverless OR Function as a Service (FaaS) deployment

Serverless deployment approach is relatively new approach and now things are moving from containerized deployments to serverless deployments. The key difference between both is how we build and package our app. I am not sure, but the underlining infrastructure of serverless deployments may be containers only. In serverless deployment, we need not to manage any server. As an app team, we don't even need to know anything about where the servers are, what are their IPs or hostnames etc.; everything is taken care by deployment service provider.

{{< image classes="fig-100 center clear" src="https://encrypted-tbn0.gstatic.com/images?q=tbn%3AANd9GcT5Oj5Cc5fj28_pGhSak2-N-PIvuR5pQLd_YQQfMbEGtk8omH0i&usqp=CAU" group="group:travel" title="Serverless Architecture" >}}

In serverless architecture, the {{< hl-text cyan >}} deployment unit is an entry point of an app {{< /hl-text >}}. You can think of an entry point of an app as any callable point in app to render a page or accept / return data (API). It's further smaller unit that microservice.

{{< image classes="fig-100 center clear" src="https://www.cloudflare.com/img/learning/serverless/glossary/function-as-a-service-faas/monolithic-application-microservice-faas.svg" group="group:travel" title="Transition from Monolithic to Serverless Architecture (Image credit: www.cloudflare.com)" >}}

##### Advantages of Serverless over containerized deployments:

* Deployments are agnostic to underlining heterogeneous infrastructure.
* As a developer, one need not to maintain or configure any servers / containers.
* Deployment unit is much smaller as compared to containers. In serverless, deployment unit is a function (an entry point for API, page etc.), where as in containerized deployments, unit of deployment is container, which may include whole app (middleware logic) or a microservice.
* As deployment unit is function (logical flow), so the change to one function does not require deployment of whole app or microservice, only the changes function is built and re-deployed. This result in much easier and faster change management.
* Most of the cloud providers charge based on function invocations - that means you are charged based on the compute time used to serve request, where as for containers they charge based on uptime of container. As a result, your cost of running app in serverless would normally be less as compared to app running in containers, unless you app is too popular and serving with full load 24x7.

##### Disadvantages of Servicerless when compared to containerized deployments:

* Deployments are kind of blackbox. You don't know where your code lives, so you loose sense of control.
* Hard to debug in production as you can not login to any server and see what went wrong. You app level logging should save you here.

### Summary

To make your web app scale-able, you need to work on both application architecture and deployment infrastructure. Key take aways:

* Deployable unit should be small (microservices or functions) and independent of other units (functional block).
* Deployable units / components should be loosely couple through APIs exposed by each component.
* Deployment infrastructure should be clustered, so that it can scale up and down on need basis.
* Use container and container orchestration or serveless approach to deploy an app, so that infrastructure can respond to scaling needs in real-time.

If you reached till this point, kudos to your reading interest. I know, no one like to read long articles, but frankly speaking, when I started writing this article, I did not plan to make it so big. I will try to keep my future articles short and crisp. I hope this article helped shape and clear some concepts in your mind. Feel free to reach me [@gaurav_dhiman](https://twitter.com/gaurav_dhiman) or at [my website](https://gaurav-dhiman.com).

***