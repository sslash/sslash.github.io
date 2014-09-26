---
published: false
---

## Working Title That Has Got Something To Do With Gardr, Ads, HTML5 and JS

Embedding advertising content on your website is an extensive task. Especially if you want to do it properly. Which you should of course, considering the vast amount of banner-content that lives on the Web today. The majority of advertising producers has started to acknowledge the fact that **Flash is dying**. This has introduced us to a new generation of (banner) content; namely HTML5. A potential pitfall here is that banners are no longer safely hidden away in a Flash container, but instead, live side by side with our belowed HTML page. This can lead to problems. 

In this article we will look at challenges with third-party content, and discuss  a sollution to these problems. A new ecosystem has emerged as a result of the new HTML5 banner generation. **We have named it Gardr**.

## The Challenge With Third-party Stuff...

Many developers have a weird relationship to front-end development. JavaScript in particular. Weirdness being overuse of copy-and-paste. Integrity to include gigantic third party libs simply in order to use one tiny feature from it. And also, many people seems to dislike JavaScript, thinking it is just a silly language that lacks proper features. Or that it is no need to learn it, because you can usually quickly google your way into the code-snippet you are looking for. This might have some unfortunate outcomes. Especially when such developers builds stuff that ends up inside an advertising container on your website. Imagine an advertising banner that accidentally changes global styling, or overrides global JavaScript objects. 

Very often advertising content is rendered inside frames. But because this solution affects the critical rendering path, many people choose to create friendly iframes. That way, advertising content can load in parallel with the rest of the async stuff on your site. However, this approach does not protect your website, because the ads can still access its parent DOM through the iframe.

## What Would Be Our Requirements?

So what are the requirements for the perfect way to embed third-party advertising content? 
     1. Don't let banners be bart of the critical rendering path. Banners must 	   render after the page has rendered so that domready can trigger early.
     2. Banner content should not be able to easily access our site's DOM. 
     3. It should be possible to have some sort of communication between the third-party content, and the host site. 

## Introducing Gardr.

At Finn.no, we have implemented a solution to this problem. Gardr. Gardr is a Javascript library that is executed after the DOM is ready. It creates an iframe on all the container positions you have chosen, and sets the iframe's source url to an HTML template that is hosted on an **external domain**. This way, the third-party banner has no access to its parent site due to **cross-domain restrictions**. The external HTML template embeds a **gardr-ext** script. This script will document write another script tag with the advertising banner's script URL. As a result, the third-party script has been bootstrapped safely inside a cross-domain iframe. Async-wise. 

In addition, Gardr offers a plugin API, so that plugins can be built to alter the behavior of the way the banner is rendered. And communicate safely with the host site. And do whatever else you would like your banner to do in order to cooperate with the site. Or the opposite.

## Let me see!!

Time to look at an Gardr. The first thing to do is to have a look at the Gardr Github project: https://github.com/gardr/. As you can see, there are many different projects here. However, you only need two:

1. gardr-host
2. gardr-ext

Gardr-host is the script you'll want to include on your site, while gardr-ext must be (well, should be) hosted on an external domain server.

Lets try them out by building a small application. We'll use yeoman just to get a quick start.




## Summary

We have looked at an efficient and safe plug-n-play solution to embedding ads and other third party content. We'we had great success with this on Finn.no. Hopefully more people will start using this. 


What's next
Open source. Participate!
Specs
Validator