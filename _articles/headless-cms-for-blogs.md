---
layout: post
title: Checking out Jekyll headless CMS for blogging
nav_order: -1 #decrease this by one for every new article
author: Marko Taponen
date: 2022-05-02
thumbnail: /assets/images/articles/1/duck-thumb.jpg
tags:
- CMS
- Jekyll
- Blogging
---

# Checking out Jekyll headless CMS for blogging

This article will demonstrate how to use Jekyll headless CMS to publish blog-type content.
<figure class="img-float-left">
  <img src="/assets/images/articles/1/duck.jpg" alt="Duck with scuba gear">
  <figcaption>Duck about to dive deep</figcaption>
</figure>

## Why headless CMS?

CMS editor is a security risk. Having all your content in a database means that you need to back it up. Also editing may break things. What breaks might not be that straightforward to understand.  You might also want to have some version control.


Headless CMS is basically a site generator that generates a website from templates and outputs pure html, CSS and JavaScript. On the actual web server there is no database, just plain static files. One could argue that you could just type them as-is. And that was the way of the world when Web 1.0 was around. In this era we need to support for example different layouts for mobile and desktop and things would get messy soon.


Downside of using this approach is that you need to have some preferrably automated deployment chain and usually the tools are programming related. Also you need to understand how the content generator you have chosen can be used and how you can add features if you need to do so. Also you cannot have rich data manipulation as that would require real backend.

We are a house full of coders. Most of us are proficient with tools like Git, various templating engines and different markup or markdown syntaxes. For our main site we have been running headless CMS for years.
What little backend-functionality we have needed, we have used serverless technologies like Lambdas.

## What is Jekyll

[Jekyll](https://jekyllrb.com/) is a headless CMS implemented in [Ruby](https://www.ruby-lang.org/en/documentation/quickstart/). It supports variety of templates most of which are free to use. You can always write your own. This page is using a template called [Just the docs](https://github.com/just-the-docs/just-the-docs) that is originally meant for generating a documentation website for your project. It provides a nice menu on the side and you can define what you want to publish (like your /docs directory content). Jekyll also supports plugins for various tasks -- like for generating rss-feed or alike.


When you write your content you can use for example markdown or html. You think about the structure of your document and leave layout to your template.

## Quick tour

![OctoJekyll](/assets/images/articles/1/octojekyll.png#img-float-right)
Easiest way to try things out is to use Jekyll with [GitHub Pages](https://pages.github.com/). GitHub Pages can be used for your project pages. It provides easy-to-setup themes. If you want to register a custom domain name that is also possible. Just make your DNS record point to the GitHub pages server, add a CNAME file to your GitHub-project and you are all set. Note that [terms and conditions](https://docs.github.com/en/pages/getting-started-with-github-pages/about-github-pages#limits-on-use-of-github-pages) apply on what can be run on GitHub pages- server, but it is fair to say that trying things out will be virtually with no cost.

## Customizing your theme

As mentioned above, you can change the theme of your Jekyll- page. Now if things are almost, but not quite perfect, you can tweak things.

Firstly - you can use [remote-themes](https://github.com/benbalter/jekyll-remote-theme). I.e. you can select a theme that is not officially supported by GitHub. If you use some other hosting-platfor you can load the theme as a gem. After that you can customize it even more by including files under `_includes`, `_layouts` and `_sass` directories of your project directory. You may want to check out the contents of the plugin you are using and "overwrite" some of the contents or alternatively use the customization points built in.

So far I have customized:
- `_includes/head_custom.html` to contain favicon
- `_layouts/post.html` to contain Author and date- information from the article
- `_sass/custom/custom.scss` to contain some styles for floating images, `figcaption`, word wrapping and index-page style
- `index.html` - custom page template for showing all the articles in a grid-layout


## The workflow
So just to make things more obvious - how does one write a blog article with this sort of setup?
[![Editor](/assets/images/articles/1/editor.png#img-float-right)](/assets/images/articles/1/editor.png) Firstly you have your favourite editor - I'm currently using MS Visual Studio Code. The article content can be in [Markdown](https://daringfireball.net/projects/markdown/) or in HTML using [Liquid-templates](https://jekyllrb.com/docs/liquid/).
You prepend your meta-information in [Front Matter-section](https://jekyllrb.com/docs/front-matter/) in the top.
Then you place your assets (pictures and such) under `assets/images` and link them in to the content.


Alternatively you might consider on integrating some [content-management tools](https://jekyllrb.com/resources/) like CloudCannon or Netlify CMS. 



I have my Jekyll running on local env using `bundle exec jekyll serve` - see [Jekyll installation](https://jekyllrb.com/docs/) for more details. I save the document and have a browser-tab open on `http://localhost:4000` to see the results.

Once I am happy on the outlooks of the article I commit my changes to git (remember also to add your image assets, template customizations and sorts) and push the changes upstream.


After that if you are on GitHub- pages the site will be deployed in few minutes. Otherwise you will need to have some sort of deployment- pipeline in place, YMMV.
What happens there in short is that Jekyll will compose a static site consisting of html and all the assets. That is deployed on a web server somewhere. And hopefully you will see what I wrote here.



## But I already have a Blog!

So you want to migrate to Jekyll? No problem. There is support for migration from multiple blogging platforms. You can use [`jekyll-import`](https://import.jekyllrb.com/docs/home/) to import the data to to your Jekyll-blog-project.
I have been using [Blogger](https://import.jekyllrb.com/docs/blogger/). Basically the xml-dump that I got from Blogger included all the article-markup. What it did not contain was all the pictures. So I just scavenged them using `wget -r http://localhost:4000 -H -D <Here Be Comma Separated List of Blogger Image Domains>` and changed my content to point to local images instead of the Blogger-hosted ones. Sorting the Blogs required bit of tweaking with `nav-order` - attribute of Front Matter. If you -- my dear reader -- can think of an easier solution, please advice me as well.


## The final conclusion

So far I have been developing and maintaining multiple different websites each with separate requirement and approaches. To me the CMS solution seems easy at first but fragile. Static sites as such are bit more difficult to set up and writing the content means that you either need some templating solution or you end up writing HTML by hand.
The headless CMS approach is bit in-between. You have the possibility of writing custom HTML should you need to. Also you can use developer-level tools like plain text editors. If you mess something up you have version control-tools on your side - nothing is lost in Git unless you have a habbit of force-pushing to main.

All in all - all that is needed now is me trying to convince my colleagues to adopt this toolkit as well.

## Links and resources
In the order of appearance

- [Jekyll Headless CMS](https://jekyllrb.com/)
- [Ruby QuickStart](https://www.ruby-lang.org/en/documentation/quickstart/)
- [Just the docs - Theme for Jekyll](https://github.com/just-the-docs/just-the-docs)
- [GitHub Pages](https://pages.github.com/) and it's [limitations](https://docs.github.com/en/pages/getting-started-with-github-pages/about-github-pages#limits-on-use-of-github-pages)
- [Markdown](https://daringfireball.net/projects/markdown/)
- [Liquid](https://jekyllrb.com/docs/liquid/)
- [Front Matter](https://jekyllrb.com/docs/front-matter/)
- [Jekyll-import](https://import.jekyllrb.com/docs/home/)





