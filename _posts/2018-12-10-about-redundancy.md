---
title: About availability and redundancy
---

The hardest problem to solve with static site generators, is availability and redundancy. In a monolithic system you would just replicate the server and you will have a complete fail-over. This is not so simple for Static Site Generators. However, you can quite easily deploy a website to multiple platforms. I have used this website as an example.

## What if the hosting is down?

- This website is available at Netlify hosting at [https://boatman-bird-64062.netlify.com/]https://boatman-bird-64062.netlify.com/).
- This website is available at CloudCannon hosting at [https://gifted-pooch.cloudvent.net/](https://gifted-pooch.cloudvent.net/).
- This website is available at Github hosting at [http://jhvanderschee.github.io/jekyllcodex/](http://jhvanderschee.github.io/jekyllcodex/).

When this website goes down, I just need to point the DNS of the domain name to another service and it is back online. This process can be automated with [DNS failover](https://dnsmadeeasy.com/services/dnsfailover/). This is a DNS system that automatically updates your records based on the availability of the endpoints in the record. Magic, right?

## What if the CMS does not work properly?

- This website can be edited directly on [Github](https://github.com/jhvanderschee/jekyllcodex).
- This website can be edited in the [Forestry.io CMS](https://forestry.io).
- This website can be edited in the [CloudCannon CMS](https://cloudcannon.com).

I can use these services all at the same time. note that CloudCannon provides different levels of access (full/code access and limited/editor access), while Forestry.io only provides limited/editor access and Github only provides full/code access.

## Then why is it hard?

In reality there is a lot more going on in a static site. It is not just the hosting and the CMS. This site, for example, uses dynamic image resizing. I use [images.weserv.nl](https://images.weserv.nl) for that. CloudCannon can solve the image resizing partially for us... but I have not seen any other CMS do that so far. Then you have forms. As you can see in the [form builder](/without-plugin/form-builder) I have implemented several form engines... and for a reason. You want to be able to easily switch your form engine. Forms can use the platform-specific solution (forms on Netlify or forms on CloudCannon), but they can also use a third party (Formspree or FormBucket). Each have their own advantages and disadvantages. 

## How to best cope with it

For important forms, I have set up an AJAX form submission before the real one, to have the forms entry duplicated. When the AJAX form submission returns an error code it nevertheless submits the real form. Setting up a failover DNS is a good measure too. In reality every service fails every now and then. The most important thing is to be aware of it, so you can take action before the important stakeholders notice the problem. To monitor uptime I use [Uptime Robot](https://uptimerobot.com). If a service goes down, Uptime Robot sends me an email. If that happens I assess what to do next. Sometimes this means that I will improve the redundancy, and sometimes I will just switch from provider.