---
layout: post
title: 【翻訳】デザインエンジニアリング
subtitle: DESIGN ENGINEERING
categories: translation
excerpt: Design Engineering - Snook.ca
---

<cite class="citation">
![Jonathan Snook](/mol/images/people/jonathan_snook.jpg)
原文：[Design Engineering](http://snook.ca/archives/opinion/design-engineering)（<time>2014-11-25</time>）by [Jonathan Snook](http://snook.ca/about/)
</cite>

> フロントエンド開発はJavaScriptだけではない。フロントエンド開発は人種のるつぼのようにデザインとディベロプメントの技術が融合したものである。それはアクセシブルなUIを実装するためであり、Web標準を受け入れるものである。— [Matt Hill](https://twitter.com/matthillco/status/480986847473303552)


When it comes to development on Shopify Admin, we have—up until recently—only had two specializations: designers and engineers. There is a third specialization, however, that has had a tough time finding a solid home: front-end developers. The skills of a front-end developer can be varied and blends into design as much as it blends into engineering. We had been very lucky to have hired talented designers who can also create high quality front-end code without the need for dedicated front-end developers.
Any talk of growing a dedicated team of front-end developers had been met with the rebuttal: “if they’re developers, then they’re part of the engineering team.” That is, all backend developers are front-end developers and vice versa. Shopify expects their developers to be full stack. But if front-end development is development, why did we have our designers do it?
The problem is that we use the terms front-end development andbackend development but people are often confused as to where a front-end developer starts and where a backend developer ends.
When we examine the development process, there are three phases: “Design”, “Design Implementation”, and “Application Development”.

Spectrum of Application Development
Design
Designers use many tools and while they should understand how their designs are implemented, it should not be a requirement for them to implement their own designs into HTML, CSS, and JavaScript. (Just as we don’t expect print designers to do their own printing. We have printers for that.) It’s advantageous when a designer can focus on multiple iterations of a design or can work through more design problems as a result of not having to focus on design implementation: the act of turning their designs into production-ready HTML and CSS.
I’ll put the clarification here that I do believe that designers should know how to code but with a growing organization comes increasing specialization.
Application Development
Application Development is about hooking up the interface and serving it in the best way possible. Should we be using a client-side MVC or server-side rendering? What’s the caching or storage system? What’s the data model? These types of concerns bleed across the HTTP barrier and shouldn’t be restricted to one side of it or the other.
Understanding OOP and prototypal inheritance requires a different set of skills than understanding how multiple browsers render a CSS property and how to best implement a design across multiple devices—phone, tablet, or desktop—and be accessible with multiple input methods—mouse, keyboard, gestures, or screenreaders.
Design Implementation
Implementing a design means writing HTML and CSS (and some JavaScript) and ensuring that the design holds up under the various design constraints: different browsers, different dimensions, different resolutions, and different interaction methods (mouse, keyboard, gestures, screen readers). It also can mean building out prototypes for UX validation. These people are design-minded but not necessarily designers. These people are technically-minded but not necessarily developers.
People in this role provide a great bridge between design and engineering. I’ve often called these people the “arbiters of design”. They inform design of possibilities and constraints and help ensure that designers build a consistent and usable interface for as many users as possible. They help codify the design work. They have a developer mindset with concerns about render performance and load times and can work with engineering to build out a performant front-end.
Roles
It’s important that we have generalists that can bleed across these lines and specialists that can go deep in each of these sections. Up until a short while ago, we were not doing enough to foster the practice of design implementation within Shopify Admin. This has been affecting our designers’ ability to focus on design and affecting our ability to hire people due to our expectation of requiring generalists over specialists.
What to call these people?
“Could front-end translate as being design engineering?” — Dan Donald
We debated on what this role should be called. Design Implementorsfelt less than impressive. We almost settled on Design Engineers but it sounded a little too “Disney”.
We also already had a well-established team of front-end developers in Toronto focused on Shopify.com and other growth projects. Their needs were a little different than ours since their front-end developers bled more into backend development.
In the end, we came back to Front-End Developer.
It was more general and enveloped all front-enders, regardless of what end of the spectrum they are at.
As an industry, though, we’re trending towards a greater specialization around design/code architecture and we’re seeing new workflows around that as we try to scale product and site development with larger teams and larger codebases, much like we’ve seen with other technologies.

