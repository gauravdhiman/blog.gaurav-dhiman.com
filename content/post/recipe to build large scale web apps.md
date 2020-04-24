---
title: 'Recipe to build large scale web apps'
date: 2020-03-21
draft: false

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

thumbnailImagePosition: left
autoThumbnailImage: true
metaAlignment: center
# coverCaption: "Datacenter"
# coverMeta: out
coverSize: full
comments: true
showTags: true
showPagination: true
showSocial: true
showDate: true
showTOCOnSide: true
---
Today web apps are developed considering global userbase, so they need to scale fast without disrruption, to serve global traffic. This post explores the architectural as well as infrastructure needs to scale any web app.
<!--more-->

## Brief history of web apps
Anyone who has worked in web application space for few years must have seen a drastic change in the way web apps are built now and then. In early days of internet, there was no concept of web apps - that was the time of static websites, followed by dynamic websites that were linked to each other with hyperlinks. I think the first web app that we could consider, would be a search engine or online directory (yellow pages). Search engine accepts some keywords and returns results on click of a button. We consider search engine as web app because that has some logic with user interface on web (in browser). From that era of heavy backend logic apps, we have come to an era where significant app logic is implemented in frontend along with backend - think of admin dashboards, web based email clients, frontend of social network - all these have a lot of UI controls, many possible user interactions and UI changes as a result of those interactions. As web apps matured over time to have all this complexity of user interface, it actually replaced the need to have a desktop apps. Things are moving fast and now even web apps are getting replaced with [hybrid apps](https://ionicframework.com/resources/articles/what-is-hybrid-app-development) and PWAs ([Progressive Web Apps](https://developers.google.com/web/ilt/pwa)).

## Problem & solution of scaling-up
System that are {{< hl-text cyan >}}rigid{{< /hl-text >}} (complex and tightly coupled components), {{< hl-text cyan >}}monolithic{{< /hl-text >}} (all in one) and are built with {{< hl-text cyan >}}no clear demarcation of functional components{{< /hl-text >}} fail to scale up. In general, to scale up any system,  we need to build a system that is {{< hl-text cyan >}}modular{{< /hl-text >}} (think of plug-n-play components), {{< hl-text cyan >}}loosely coupled{{< /hl-text >}} and {{< hl-text cyan >}}flexible{{< /hl-text>}} (react to changes). This principal is not specific to software systems, but to all kind of systems - think of factories, airports, hospitals, government / political systems. The more you observe how real world systems work, the better system designer you can be and software system design is not in anyway different from it.

To scale up software systems, we need to think of components from two different perspectives {{< hl-text cyan >}}architectural{{< /hl-text >}} and {{< hl-text cyan >}}deployment infrastructure{{< /hl-text >}} perspectives. Let's cover each of these in detail.

### Architectural considerations
Architecturally scale-able applications should have smaller, reusable and independent components that are loosely couples (free to move around n larger system design). Think of how small lego pieces of different shapes and colors are used to build something big and meaningful. Same way software systems should be build with small components that have plug-n-play interfaces.

{{< image classes="fig-100 center clear" src="https://images.unsplash.com/photo-1568617934289-df4399f8cea3" group="group:travel" title="Photo by Dan Burton on Unsplash" >}}

Any web app can be logically divided into mainly three tiers - front-end (UI/browser), middleware (app server) and database server. Earlier middleware server layer used to be monolithic (all app logic as single deployable unit). To scale the traditional web app, we used to deploy multiple instances of whole monolithic app either on physical or virtual machines. This was not optimal and great way to scale. This was traditional way of building app ([monolithic architecture](https://www.youtube.com/watch?v=MPpU8y3ykS4)). To explain it better,think of an app having few services - **authentication**, **user**, **product**, **order** etc. In monolithic architecture, single unit of deployable will have whole app (middleware server), including all the services. Whenever we need to run another instance of app, we need to deploy the whole app (monolithic way). Single unit of deployment in monolitich app look like below.

{{< image classes="fig-100 center clear" src="https://lh3.googleusercontent.com/_Jtqzvnp3ELXaUxpDhzDffdMhX-WmpWkz20UsJ1_QEmR7DaHwS3ew_ZuBlYho4b1MzY6lO7gkDpf0Qvvw0RS5iOSRtDLupRKojXgOK4_i2Mh9VQwiUvRUG8Vc5cJWjxNAFj9Bq2hBnm5HVBIxlgD13Bjg4UoKHvclAEZ0Vdfipxtn_LVE5y6B7mS2u5bxGYpg_zKQOsql2blsSH27uDgjx2212MRvbzjUtYWjYNg2KaLfPk6Ghn1Nt3LSKzvxZq5RTkV0G9t9iJu6gJjLMBGpAg7YYgVv98j1J6JreRVX0wGqSP0JDNRw0USivTPpo-ZsYYgdyIi5QqHyrA9OuDJkSa1ShMn00k_AzhX7Gewc7hvXCrgbbWLKxC1nO2XfNjvPN3135DSJTdFGxAwU7GsZFMlt3h8m-ZFdGbo6IUhPLSto8v8oK9OWllJB7tujkUpWwuNKpabJHU7dNUNtNIwtSb7k9gTPCbyH7V4iT60_F_mjnm7obQsuV5oAtfY-h46PsvpYRskYrniymi9afz5SNTte4ic-ZU4B3zf1QnmR9osi7ooSwhKWkpeKwDLHlGdNV7Ig--J3Mmx0tJc1U9Z0g7Pkdt8_67QAiXjPhHqJ2ckx9hrpK5q-CTcqPvJDCcPfwsZMOIhJDIDdHBJ6B6ixQ-YY8BccWLPBjn-UrswVJRTZH6u3rFLgNk92WBX7Q=w2290-h1327-no" group="group:travel" title="Monolithic Architecture" >}}

If one or more services are more used in application as compared to others, then why we need to deploy less used services with each deployment (app instance) - no point of scaling the service which is hardly or less used. We need to scale up the components of app that are more used (get more web traffic). For instance, {{< hl-text cyan >}}order service{{< /hl-text >}} would not be as heavily loaded as {{< hl-text cyan >}}product service{{< /hl-text >}}. Order service will be used only by logged in users who wants to buy a product, where as the product service will be used by both logged-in and non-logged-in users to view the product details on product page. With this understanding, we should have made each service as independent and loosely couple unit of deployment. This is known as [microservices architecture](https://docs.microsoft.com/en-us/azure/architecture/guide/architecture-styles/microservices), where each service (logical unit of business function) is a independently deployable unit. Below diagram shows the same.

{{< image classes="fig-100 center clear" src="https://lh3.googleusercontent.com/4mHRQGQWOW_itf2L0vu_CSBVjGOfjCGvNJZucokkZdBAfugUFgWH9BZR3ZG1webchGSNo7l5EpPLCcSMWmo_YGUP5MstvvcTV138Dke2JHMUfatg8Sg_h6LNnTHBb-YOaEmsnYnOoPcPGEK1ErU4mnTenH-_yWlXImuw3-PsrlKFtG-ihY1ajuTp3G_BPKZJvYl8lePdR6mCXxBecffAFZ4do7D4meJgdwnzGK_nFRYHodnYmdTz1ufwx5nn7xOOFSCqEH-_8eJoSU_opXqDw4-IXLoQtgLQAF7C8p1VAmJ9iue2h7eVSfnKzHs0Ds6IZdzbKHoCfZSbU74bBLio7iDC_wKgYCaXn7ARuYjNkdVMxlSsVNVLEpMfEzG50xqx8igUWHpORE-mzjK5O91rOV39LPW45Jfxms-W1mc0Ow_K__r06B9udCC3rjH8aH8YqJdeMbsROPWiLBSxNXWEhyCi1nCKM8Jhmm4gEAltZ6vSjlfuiChGw7R6m3eTuBQG-Z4Ibca3tgPmIoxj2kiyC4ZipoTMiyOOSzt_K7k-ysJc8fvWGe9UBwLm7NGHG7r1UlQVfcWMDL6a0sT7_7enY8c6VPLuwJxjPoSdKgzRfMlmeERRinuiBfK447nLK8q_P3jMRg0PrEUDzscWHCxUcUS-DuIuuAWcAfi1JIY1wcFHlKUo95ZO1hyf0TV5jg=w1837-h1802-no" group="group:travel" title="Monolithic Architecture" >}}

Below diagram sums-up the difference between monolithic and microservices architetures. Here you can see, in monolithic architecture everyhing is packaged in every single instance of deployment, where as in micoservices, the application is broken down into small functional unIt's (microservices) and each of those can be deployed separately and scaled-up based on which gets more demand / traffic.

{{< image classes="fig-100 center clear" src="https://dannyvanderkraan.files.wordpress.com/2017/02/serverless-on-azure-figure-5-2.png" group="group:travel" title="Monolithic vs Microservices Architecture" >}}

Same as middleware (server app), database layer also needs to be scale-able to make the whole app scale-able. To make database scalable, it needs to be running on cluster of nodes, all nodes being configered as active-active with data getting sheredded over all nodes. Cluster management takes care of scaling up the cluster size by including new nodes in the cluster without any downtime. While architecting scale-able apps, one should choose the database that is distributed and can run in active-active cluster.


### Deployment infrastructure considerations
Along with application architecture, the underlining infrastructure plays a huge role in making the app truely scale-able. Even the well architected microservices based web app can not scale if the underlining deployment infrastructure is not scale-able. In this section I will talk more about deployment strategy. Technology and tools for deployment and managing infra has changed drastically in last few years, mainly in last 15 years. Below diagram shows the snapshot of change from traditional way of deployment on physical servers to virtualized deployments to containerized deployments.

{{< image classes="fig-100 center clear" src="https://www.scaleway.com/assets/images/docs/kube-intro/Deployment_Evo.png" group="group:travel" title="Changes in deployment approach over years. (Image credit: www.scaleway.com)" >}}

#### Deployment on physical server environment
Long back, web apps used to get deployed on few PMs (Physical Machines). Managing and scaling PMs was more of a manual job, so not scale-able in true sense. This required lot of advanced planning before the spike in traffic happens. Scaling up and down was not possible in real time on need basis. Below daigram show the traditional deployment where application gets deployed on physical machines.

{{< image classes="fig-100 center clear" src="https://lh3.googleusercontent.com/o2c1WKWjH_OasaADJ4OHTk45FvDyDcL0qXKqN_Z8arl1rJkv4dSP0wv2YA90n8ct_fozsGfajCg_SzKGMfw2jazlDYEteHZzKNYjg2m014I3Qym9sUDsDz29hX2S2iZkLvChzuMYBrSbTkM_0sgBkUPTIJ2E6KwjJ7Ba-zbakxLnej8b2PAFVi6hk0Rbb5mx30DuhpjYCktEcnC_K9vsNPtMZxwxt00yq-Vvc3C99Q1cSzL_uiq-dnLssMWAxqiDWrlfdv5wpE0seXRzAEcY5PAhafM8k8sbO3SL_MYdmwKhIGGRvyZe9Cvj6QNTIgIw641KIe8Kahlia9H9S-Pjn5oJkup3EiMf_TkbvadeO2pCCE6mEonXD-HRvg39aJVNytdOGwMjvMSFgSQ0GGaJr9biCTGeCh16qW_Zdw5T8rCmdDL0wPyRGKHBI8VN-K93coM_4rXPWKXDHL-hWBoZtxmiEMDbrJ11fD0dl7siAkOLDNIaKfIxveAYqDROSXvZHyMVV0b02tVj0tAaRj_c6dwrzW6-jbmk8h4TsfjVDyA7N0ZQeCsnIxAauo9WgfctM-scjt49_jt8EXLdqAKjnWKozS0qWihV1NlnIojTD2jk4O38dDRzzTfE5jL196kHQIBLTUyBmQTO1H7BewNCSs8p6ybXmg4J8wt8UHW5r3NN2-UHZst2rbHko-sU_A=w1837-h1570-no" group="group:travel" title="Physical servers cluster." >}}

#### Deployment on virtualized environemnt
Then came the time of VMs (Virtual Machines). Advantage of VMs over PMs was better resource utilization and near to real-time response to scaling up needs. One PM can host multiple VMs based on what resources those VM needs, so where we used run one instance of an app in one PM, we can run multiple instances of an app in case of VMs on same PM. This results to better harware resource utilization. As VMs are also relativily quicker to boot and brought into network, scaling up in real-time was also addressed. When traffic spikes, the underlining VM management software spins up multiple VMs, hosting the app instance and bring them on network in near to real-time manner. When traffic lowers down, it can shutdown the VMs. Network typologywise, virtualized deployment schema looks similar to physical deployment schema, except that on each PM there will be multiple VMs. Below diagram shows how multiple VMs are hosted on single PM.

{{< image classes="fig-100 center clear" src="https://miro.medium.com/max/2396/1*oF6QqYRhWPw9HF20CUqhMw.png" group="group:travel" title="Multiple VMs on same PM. (Image credit: www.medium.com)" >}}

#### Containerized deployment
VMs were better than PMs but they were still resource intensive for the task of running an app instance. Each VM requires space and memory for Guest OS, common utilities in addition to web app and It's dependent packages. Also becuase of this bloatted image of VM, booting VM and making web app available to user takes some time (few minutes at least), so there was always a scope of improvement over VMs. As an improvement to VMs, idea of containerization came in. [Container](https://www.youtube.com/watch?v=0qotVMX-J5s) is packaging of app along with It's dependent packages / libraries, without any overload of guest OS and other low level stack. You can think of container as a light-weight VM, that boots fast and make the app instance available in few seconds than minutes as in case of VMs. Below diagram shows the multiple containers hosted on single physical machine. [Docker](https://docs.docker.com/get-started/overview/) is one of the most popiular containerization software that manages the life-cycle of a container.

{{< image classes="fig-100 center clear" src="https://www.docker.com/sites/default/files/d8/styles/large/public/2018-11/container-what-is-container.png?itok=vle7kjDj" group="group:travel" title="Containers. (Image credit: www.docker.com)" >}}

To manage multiple containers and ensure that they scale up and down as and when required, another cluster aware software is used - in general term that is known as [container orchestration](https://www.youtube.com/watch?v=kBF6Bvth0zw) software. [Kuberneties](https://www.youtube.com/watch?v=PH-2FfFD2PU) is one of the popular container orchestration cluster management software. It ensure that the given cluster configuration is always mantained in run time. Below diagram shows high-level architeture of Kuberneties and how it manages the pods (run time container image) using Docker. In the below diagram, {{< hl-text cyan >}}Node{{< /hl-text >}} represents a single physical or virtual machine. Master node is a management / admin node in cluster and worker nodes / machines are compute nodes (hosts for pods), each one having a container management software (Docker in this case) installed on it. Docker on each worker node is responsible to manage the life-cycle of containers on that node. Kuberneties talk to Docker through {{< hl-text cyan >}}kubelet{{< /hl-text >}} (you can think of them as agent components). They relay commands from API server to Docker on given node. In case you want to learn more about containers and container orchestration and how they cmompliment each other, watch this short [video about Dockers and Kubernities](https://www.youtube.com/watch?v=2vMEQ5zs1ko). 

{{< image classes="fig-100 center clear" src="https://res.cloudinary.com/dukp6c7f7/image/upload/f_auto,fl_lossy,q_auto/s3-ghost/2016/06/o7leok.png" group="group:travel" title="Kubernities Architecture. (Image credit: www.docker.com)" >}}

After going through all above, we can easily see how the deployment infrastructure has changed over period and how reactive and scale-able the deployment inftastructure has become, leveraging the cluster capabilities.

#### Serverless OR Function as a Service (FaaS) deployment
Serverless deployment approach is relatively new approach and now things are moving from containerized deployments to serverless deployments. The key difference between both is how we build and package our app. I am not sure, but the underlining infrastructure of serverless deployments may be containers only. In serverless deployment, we need not to manage any server. As an app team, we don't even need to know anything about where the servers are, what are their IPs or hostnames etc.; everything is taken care by deployment service provider.

{{< image classes="fig-100 center clear" src="https://encrypted-tbn0.gstatic.com/images?q=tbn%3AANd9GcT5Oj5Cc5fj28_pGhSak2-N-PIvuR5pQLd_YQQfMbEGtk8omH0i&usqp=CAU" group="group:travel" title="Serverless Architecture" >}}

 In serverless architecture, the {{< hl-text cyan >}} deployment unit is an entry point of an app {{< /hl-text >}}. You can think of an entry point of an app as any callable point in app to render a page or accept / return data (API). It's further smaller unit that microservice.

 {{< image classes="fig-100 center clear" src="https://www.cloudflare.com/img/learning/serverless/glossary/function-as-a-service-faas/monolithic-application-microservice-faas.svg" group="group:travel" title="Transition from Monolithic to Serverless Architecture (Image credit: www.cloudflare.com)" >}}
 
##### Advantages of Serverless over containerized deployments:
* Deployments are agnostic to underlining hetrogenious infrastructure.
* As a developer, one need not to mantain or configure any servers / containers.
* Deployment unit is much smaller as compared to containers. In serverless, deployment unit is a function (an entry point for API, page etc.), where as in containerized deployments, unit of deployment is container, which may include whole app (middleware logic) or a microservice.
* As deployment unit is function (logical flow), so the change to one function does not require deployment of whole app or microservice, only the changes function is built and re-deployed. This result in much easier and faster change management.
* Most of the cloud providers charge based on function invocations - that means request to your application, where as for containers they charge based on uptime of container. As a result, yur cost of running app in serverless would normally be less as compared to app running in containers.

##### Disadvantages of Servicerless when compared to containerized deployments:
* Deployments are kind of blackbox. You dont know where your code lives, so you loose sense of control.
* Hard to debug in production as you can not loging to any server and see what went wrong. You app level logging should save you here.

### Summary
To make your web app scale-able, you need to work on both application architecture and deployment infrastructure. Key take aways:
* Deployable unit should be small (microservices or functions) and independent of other unIt's (functional block).
* Deployable unIt's / components should be loosely couple through APIs exposed by each component.
* Deployment infrastructure should be clusterd, so that it can scale up and down on need basis.
* Use container and container orchestration or serveless approach to deploy an app, so that infrastructure can respond to scaling needs in real-time.
****