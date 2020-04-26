+++
autoThumbnailImage = false
categories = ["Technology"]
clearReading = true
comments = true
coverImage = ""
coverSize = ""
date = 2020-01-05T07:00:00Z
draft = true
keywords = ["Serverless Deployment", "JAMStack", "Blog"]
metaAlignment = ""
showDate = true
showPagination = true
showSocial = true
showTOCOnSide = true
showTags = true
tags = []
thumbnailImage = ""
thumbnailImagePosition = ""
title = "How I setup a blog on my domain with almost no cost."

+++
Blogging is nice habit, if you like to share the skills, knowledge and your thoughts with wider audience. Sometime people blog just to keep their notes and thoughts handy, that is good too. I used to blog long back, somewhere in 2004 to 2007. At that time, I had two blogs - one was [Linux Kernel blog](http://lkdp.blogspot.com/) hosted on Blogspot and another one was was more of [personal blog](https://gauravd.wordpress.com/) hosted on Wordpress. Somewhere in 2008 I left blogging and just got occupied with other stuff in life - career, family, kids etc. Now with beginning of 2020 I thought I should get back to blogging and try to keep it a regular feature in my life, let's see how far I can go this time 🤞.

Although there are much better blogging platforms (Medium and LinkedIn Articles) now as compared to what it used to be earlier, but still this time I thought to setup the blog on my own domain that is self-managed and self-hosted.

For self-hosting, I wanted the blogging software that is:

* Quick to setup - no hassle of setting up web-server or database, so bulky software like Wordpress and Ghost were out of option. I kept my options limited to JAMStack. You can check all options here.
* Option of writing posts with Markdown - it is simple yet powerful enough for writing documents.
* I wanted to have seamless and preferably serverless continuous deployment setup, so that I just need to work on my blog posts and as soon as I push it to my repo, it immediately gets deployed on my domain.

Considering these requirements, I started exploring [JAMStack](https://jamstack.org/) options as it does not require any web-server and database to work. JAMStack site is a static site that is generated when you build your app. There are [many options available](https://www.staticgen.com/) when you go this way.

Out of few options that I evaluated, I chose [Hugo](https://gohugo.io/), the static site generator written in Go language. It is a popular [JAMStack]() option to build websites and blogs. Few reasons for choosing Hugo was:

* It's popularity on Github. It has more than 43,000 stars.
* Its simplicity. Within a minute you can have it running in your local environment.
* You have an option to choose template from vast [collection of free templates](https://themes.gohugo.io/). For my blog, I chose [this template](https://themes.gohugo.io/hugo-tranquilpeak-theme/).

For hosting and deployments, I chose [Zeit.co](https://zeit.co/), a cloud hosting provider, leveraging serverless deployment approach. Its also a company that is behind popular [NextJS](https://nextjs.org/) framework. I have earlier hosted few applications (like [my personal website](https://www.gaurav-dhiman.com) and [real-time progressive web app](https://discussion.im) for online discussion forums) using their seamless deployment pipeline and I just love the simplicity of it. Zeit have a [free hosting plan](https://zeit.co/pricing) with all the cool features of custom domain, continuous deployments with GIT, hosting of unlimited websites and benefits of serverless deployments.

Finally here is the short list of things I selected.

## Table

| Item | Pricing |
| :---: | --- | --- |
| Bought domain from GoDaddy | $1 |
| Hugo as blogging software | Free and open-source |
| Zeit.co for hosting and deployments | Free plan |

For self-hosting I wanted something that I can quickly host and have more control over. I did not want to use bulky blogging software (like [Wordpress](https://wordpress.com/) or [Ghost](https://ghost.org/)) that requires some web server and database setup, so I kept my options limited to [JAMStack](https://jamstack.org/) static site generators. There are [many options available](https://www.staticgen.com/) when you go this way. I also preferred to have deployments done [Zeit.co](https://vercel.com/), a serverless deployment company that also developed [NextJS](https://nextjs.org/). I have hosted few applications (like [my personal website](https://www.gaurav-dhiman.com) and [real-time progressive web app](https://discussion.im)) using their seamless deployment pipeline and I just love the simplicity of it. Keeping Zeit deployment experience in mind, I wanted my blog also to be hosted and deployed using Zeit.

Out of few options that I evaluated, I chose [Hugo](https://gohugo.io/), the static site generator written in Go language. It is a popular [JAMStack]() option to build websites and blogs. Few reasons for choosing Hugo was:

* It's popularity on Github. It has more than 43,000 stars.
* Its simplicity. Within a minute you can have it running in your local environment.
* You have an option to choose template from vast [collection of free templates](https://themes.gohugo.io/). For my blog, I chose [this template](https://themes.gohugo.io/hugo-tranquilpeak-theme/).

There are many options if you want to self host your blog. I will talk bout some of those before telling what I choose for my blog.

## Popular blogging platform to explore:

This is the quickest way of to get your blog up and running. You don't need to worry about hosting, upgrading or setting up some technical infrastructure for it. You simply register on one of the blogging platforms, choose your template and start blogging, but this comes at some monthly running cost. I would recommend you to go for this, if you are not concerned about some running cost every month. Here is the list of some popular blogging platform.

* [Medium](https://medium.com) - This has made the blogging a fun. Authoring and editing your blog has never been so easy. One of the great things about this is that it's Ad free. By keeping it Ad free and by hosting great content with clutter free UI, it has become a blogging platform of choice for many. It hosts blogs about almost every subjects from people of varied backgrounds. Although it's Ad free but it has some [revenue model](https://blog.medium.com/the-medium-model-3ec28c6f603a) to keep the shop running.
* [LinkedIn Articles](https://www.linkedin.com/help/linkedin/answer/47538/publish-articles-on-linkedin?lang=en) - This is another great place where you can share your knowledge. Being a professional networking site, sharing skills and knowledge here makes more sense. It will help you build your online reputation and get you some great connections that may help you in your career path. From authoring perspective, it's very similar to Medium - clean clutter free UI and great user experience (UX) for both authors and readers.
* [Ghost](https://ghost.org/) - This is another great blogging software that if already hosted for you. It's bit costly for a blogger who just starting off. Again, it has very clean UI / UX. It has a lot of templates to choose from and

Blogging is a nice way to share your skills, knowledge and thoughts with people of same interest. It allows people to build their online reputation, and also make themselves visible to larger audience. Once people recognize you for specific skill or the knowledge you hold of specific domain, that brings you new opportunities in your carrier path.

I used to blog long back, somewhere in 2004 to 2007. At that time, I had two blogs - [technical one on blogspot](http://lkdp.blogspot.com/) and [personal one on wordpress](https://gauravd.wordpress.com/). Somewhere in 2008 I left blogging and just got occupied with other stuff life - carrier, family, kids etc. Now with beginning of 2020 I thought I should get back to blogging and try to keep it a regular feature this time. In last one decade things has changed a lot overall. Same is true for blogging platforms too. Now we have much advanced blogging platforms like [Medium](https://medium.com/) and LinkedIn with a flavor of social networking added to it.