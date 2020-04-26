+++
autoThumbnailImage = false
categories = ["Technology"]
clearReading = true
comments = true
coverImage = "https://images.unsplash.com/photo-1455390582262-044cdead277a?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1932&q=80"
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
thumbnailImage = "https://images.unsplash.com/photo-1455390582262-044cdead277a?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1932&q=80"
thumbnailImagePosition = "left"
title = "How I setup a blog on my domain with almost no cost."

+++
Blogging is nice habit, if you like to share the skills, knowledge and your thoughts with wider audience. Sometime people blog just to keep their notes and thoughts handy, that is good too. I used to blog long back, somewhere in 2004 to 2007. At that time, I had two blogs - one was [Linux Kernel blog](http://lkdp.blogspot.com/) hosted on Blogspot and another one was was more of [personal blog](https://gauravd.wordpress.com/) hosted on Wordpress. Somewhere in 2008 I left blogging and just got occupied with other stuff in life - career, family, kids etc. Now with beginning of 2020 I thought I should get back to blogging and try to keep it a regular feature in my life, let's see how far I can go this time 🤞.

Although there are much better blogging platforms now as compared to when I used to blog earlier, but this time I thought to setup the blog on my own domain that is self-managed and self-hosted.

## What I needed from my blogging software?

* Quick to setup - no hassle of setting up web-server or database, so bulky software like [Wordpress](https://wordpress.com/) and [Ghost](https://ghost.org/) were out of option.
* Option of writing posts with [Markdown](https://www.markdownguide.org/) - it is simple yet powerful enough for writing online documents.
* I wanted to have seamless and preferably [serverless](https://en.wikipedia.org/wiki/Serverless_computing) continuous deployment setup, so that I just need to work on my blog posts and as soon as I push it to my repo, it immediately gets deployed on my domain.

Considering these requirements, I started exploring [JAMStack](https://jamstack.org/) options as it does not require any web-server and database to work. JAMStack site is a static site that is generated when you build your app. There are [many options available](https://www.staticgen.com/) when you go this way.

### What I chose?

Out of few options that I evaluated, I chose [Hugo](https://gohugo.io/), the static site generator written in Go language. It is a popular JAMStack option to build websites and blogs. Few reasons for choosing Hugo was:

* It's popularity. It has more than 43,000 stars on Github.
* Its simplicity. Within a minute you can have it running in your local environment.
* You have an option to choose template from vast [collection of free templates](https://themes.gohugo.io/). For my blog, I chose [this template](https://themes.gohugo.io/hugo-tranquilpeak-theme/) because of its clutter free UI/UX.
* Support for Google analytics as you may want to know your audience better.
* Support for [Disqus](https://disqus.com/) comments.

For hosting and deployments, I chose [Zeit.co](https://zeit.co/), a cloud hosting provider, leveraging serverless deployment approach. Its also a company that is behind popular [NextJS](https://nextjs.org/) framework. I have earlier hosted few applications (like [my personal website](https://www.gaurav-dhiman.com) and [real-time progressive web app](https://discussion.im) for online discussion forums) using their seamless deployment pipeline and I just love the simplicity of it. Zeit have a [free hosting plan](https://zeit.co/pricing) with all the cool features of custom domain, continuous deployments with GIT, hosting of unlimited websites and benefits of serverless deployments.

### How much it all costed me?

| Item | Pricing |
| :---: | --- |
| Bought domain from GoDaddy | $1 |
| Hugo as blogging software | Free and open-source |
| Zeit.co for hosting and deployments | Free plan |

So over all cost of my blog setup is $1 per year. Now you know the recipe too, feel free to setup your own blog and share feedback, if any. If you think self-hosting is not your cup-of-tea I would recommend you to use hosted solutions.

## Other options to explore:

I preferred self-hosting, but if that is something you do not prefer, choosing one of the hosted platforms is the quickest way of to get your blog up and running. You don't need to worry about hosting, upgrading or setting up some technical infrastructure for it. You simply register on one of the blogging platforms, choose your template and start blogging, but this comes at some monthly running cost. Here is the list of some popular blogging platform.

* [Medium](https://medium.com) - This has made the blogging a fun. Authoring and editing your blog has never been so easy. One of the great things about this is that it's Ad free. By keeping it Ad free and by hosting great content with clutter free UI, it has become a blogging platform of choice for many. It hosts blogs about almost every subjects from people of varied backgrounds. Although it's Ad free but it has some [revenue model](https://blog.medium.com/the-medium-model-3ec28c6f603a) to keep the shop running.
* [LinkedIn Articles](https://www.linkedin.com/help/linkedin/answer/47538/publish-articles-on-linkedin?lang=en) - This is another great place where you can share your knowledge. Being a professional networking site, sharing skills and knowledge here makes more sense. It will help you build your online reputation and get you some great connections that may help you in your career path. From authoring perspective, it's very similar to Medium - clean clutter free UI and great user experience (UX) for both authors and readers.
* [Ghost](https://ghost.org/) - This is another great blogging software that is already hosted for you. It's bit costly for a blogger who just starting off. Again, it has very clean UI / UX. It has a lot of templates to choose.

Even if you self-host your blog, it's good idea to re-publish your post on these popular platforms to get some readers attention as these platforms are common places for avid readers.

I hope you liked reading this post and learned something out of it. Keep exploring. Feel free to reach me [@gaurav_dhiman](https://twitter.com/gaurav_dhiman) or at [my website](https://gaurav-dhiman.com).