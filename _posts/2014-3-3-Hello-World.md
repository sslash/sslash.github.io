---
published: false
---



## Hello, HTML5 Ads

Embedding advertising content on your website is an extensive task. Especially if you want to do it properly. Which you should of course, considering the vast amount of banner-content that lives on the web today. The majority of advertising producers have started to acknowledge the fact that Flash is dying. This has introduced us to a new generation of (banner) content; namely HTML5. A potential pitfall here is that banners are no longer safely hidden away in a Flash container, but instead, live side by side with our belowed HTML page. This can lead to problems. 

In this article we will look at ways to incorporate such third party content to a website, and we will discuss a new ecosystem that has emerged as a result of this new banner generation; namely Gardr.

## The Challenge

Many developers have a weird relationship to front-end development. JavaScript in particular. Weirdness being overuse of copy-and-paste. Integrity to include gigantic third party libs simply in order to use one tiny feature from it.  Also many developers lack interest in JavaScript itself, thinking it is just silly language that lacks proper features. Or that it is no need to learn it, because you can usually just google your way into the solution you are looking for. This might have some unfortunate outcomes. Especially when such developers builds stuff that ends up inside an advertising container on your website. Imagine an advertising banner that accidentally changes global styling, or overrides global JavaScript objects. 

Very often advertising content is rendered inside frames. But because this solution affects the critical rendering path, many people choose to create friendly iframes. That way, advertising content can load in parallel with the rest of the async content your site needs. However, this approach does not protect your site, because the ads can still access its parent DOM through the iframe.

## The Requirement

So what are the requirements for the perfect way to embed third-party advertising content? 
     1. Don't let banners be bart of the critical rendering path. Banners must 	   render after the page has rendered so that domready can trigger early.
     2. Banner content should not be able to easily access site's DOM. 
     3. It should be possible to have some sort of communication between the third-party content, and the host site. For instance to let the host site alter the containers that wraps the banners, if needed.

## Introducing Gardr.

At Finn.no, we have implemented a solution to this problem. Gardr is a Javascript library that creates an iframe and sets the source url to an HTML template that is hosted on an external domain. Then it document writes a script tag that has the advertising banner's URL, into the iframe. This way, the third-party banner have no access to its parent site due to cross-domain restrictions. 

In addition, Gardr offers a plugin API, so that advertising banners has a chance to all the neat things it needs to do. Like resizing its container. Or become sticky. 

## Let me see!!

Time to look at an Gardr. The first thing to do is to have a look at the Gardr Github project: https://github.com/gardr/. As you can see, there are many different projects here. However, you only need two:

1. gardr-host
2. gardr-ext

Gardr-host is the script you'll want to include on your site, while gardr-ext must be (well, should be) hosted on an external domain server.

Lets try them out by building a small application. We'll use yeoman just to get a quick start.




## Summary

We have looked at an efficient plug-n-play solution to embedding ads. We'we had great success with this on Finn.no. Hopefully more people will start using this. 


What's next
Open source. Participate!
Specs
Validator