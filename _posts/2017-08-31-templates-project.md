---
layout: post
title:  "An open source project for notification templates?"
date:   2017-08-31 02:00:00 +0100
banner_image: Fotolia_118437056.jpg
author: David Brown
comments: true
---
*By [David Brown](https://twitter.com/BDavid24)*

To set the context, I'm [on a mission](https://notifme.github.io/notifme-blog/2017/08/22/genesis.html) to help startups improve the quality of their communication with their users. Today I have a question about the templates of your transactional notifications (email, SMS, push, webpush...).

I think templates should be handle inside the code, but should be editable by anyone on the team, which is not possible at the moment. I'd like to start an open source project tackling that, but I'd like to be sure that it's a real problem.
<!--more-->

## The case

### 1. Templates should be in the code

As a developer I want the control over what's happening in the application, and I strongly believe that transactional notification templates are part of the application. Here is why, in my view:

* **Variables replacement** — When I pass parameters to render a template, I know what I'm doing. If I edit a template, I know which variables I can use and add one if I need it. If one is not necessary anymore, I remove it.
* **Versioning system** — When I deploy to production, I want to control which version of what is running to ensure the consistency of the system.
* **End to end tests** — When I test the "lost password" feature for example, I don't want to use the production (or sandbox) account to receive a real email, I just want to view the result locally in my notification catcher to click on the link.
* **Code quality and consistency** — When templates are not in the code (maybe on a SAAS), I can't enforce the same rigor than in the rest of the code. If a closing tag is missing or indentation is messy, I may not even kwow.

### 2. Templates should be editable by marketers, customer service, translators, etc.

Everyone on the team should be able to edit or propose a modification, whether someone from the customer service have seen a typo or a marketer wants to change an image. This:

* **Improves quality**
* **Allows faster iterations** — In autonomy.
* **Loosens bottlenecks** — No need to depend on the busy developer team.

### 3. The current way(s) to go

Currently this is a decision that every company is making: let developers handle templates or use a SAAS solution.

If we want to answer both of these points, the only available solution that I know of is **_having everyone on the team knowing is way around code_**. Easy, right?

### 4. The idea

> Wouldn't it be perfect to have an in-house tool allowing template edition, localization, and previewing by non-tech, and have this tool generate code and pushing to git? That would allow the use of devtools (code format, code linting, unit tests, code reviews) on everyone's enhancements.

## Do you have the same problem?

From my experience I think such a tool would be a must have, but well, as much as I'd like to start coding an open source project to implement it, I'm not really sure it's a real pain point for enough people.

So: good idea or not? I created an empty repository [notifme-template-ui](https://github.com/notifme/notifme-template-ui) to validate that.

I think 2000 stars is a very good number, if the repository reaches that, I'll be happy to start coding :)

<p align="center">
  <img src="../../../assets/2017-08-31-templates-project/idea.gif" alt="Good idea?">
</p>
