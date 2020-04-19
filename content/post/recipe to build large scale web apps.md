---
title: 'Recipe to build large scale web apps'
date: 2020-04-19T17:18:05+01:00
draft: false
---

# Some history of web apps:
Anyone who has worked in web application space for few years must have seen a drastic change in the way web apps are built now and then. In early days of internet, there was no concept of web apps - that was the time of static websites, followed by dynamic websites that were linked to each other with hyperlinks. I think the first web app that we could consider, would be a search engine - that accepts some keywords and returns results on click of a button. We consider search engine as web app as that had some logic with user interface on web (in browser). From that era of heavy backend logic apps, we have come to an era where significant app logic is implemented in frontend along with backend - think of admin dashboards, web based email clients, frontend of social network - all these have a lot of UI controls, many possible user interactions and UI changes as a result of those interactions. As web apps matured over time to have all this complexity of user interface, it actually replaced the need to have a desktop apps. Things are moving fast and now even web apps are getting replaced with hybrid apps (apps that can get installed on your desktop, mobile or can even be accessed over web) - think of PWAs (Progressive Web Apps).

# Problem of scaling-up:
System that are rigid (complex and tightly coupled component interfaces), monolithic and are built with no clear demarcation of functional components fail to scale up. In general, to scale up any system,  we need to build a system that is modular (think of plug-n-play components), loosely coupled and flexible (react to changes). This principal is not specific to software systems, but to all kind of systems - think of factories, airports, hospitals, government / political systems. The more you observe how real world systems work, the better system designer you can be and software system design is not in anyway different from it.

To scale up software systems, we need to think of components from different perspectives in the whole life-cycle of an application (development, testing, deployment and run-time phases). We need to make every phase scale-able; esp. run-time. At the same time, we also need to think from __architectural__ and __technical infrastructure__ perspective. Let's cover each of these in detail.

## Architectural considerations:
Architecturally scale-able applications should have smaller and independent components. Think of how small lego pieces of different shapes and colors are used to build something big and meaningful. Same way software systems should be build with small components that have easy to plug-n-play interfaces.

{{< image classes="fig-100 center clear" src="https://images.unsplash.com/photo-1568617934289-df4399f8cea3" group="group:travel" title="Lego blocks" >}}