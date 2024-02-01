---
title: "Updating This Blog: Hugo and Theme"
date: 2024-02-02T01:43:59+09:30
Tags: ['hugo','blog','scss']
---

* [Content Repo](https://www.youtube.com/watch?v=L0nRFNWD4p8)
* [My Anatole Fork Repo](https://github.com/Rhiyo/runecaster-java)
* [Anatole Theme](https://github.com/Rhiyo/runecaster-java)

thisisthestartofsummary

# The Foundation of the Blog

This post outlines the journey of updating my blog, a story I realized I've never shared—the original construction of this site. Embarking on this project was more daunting than anticipated, encompassing both the initial setup and the subsequent updates. Thus, detailing this experience seemed necessary.

In 2020, amidst job searching, I sought a digital space to display and discuss my projects—a hybrid of a portfolio and a blog. This space was intended for tutorials, updates on my endeavors, or any topic of interest, essentially an "everything blog."

While I could have opted for any blogging platform, my path led me to static site generators, striking the perfect balance:

* Code customization was possible.
* It allowed for self-hosting.
* The site was fast, generated at deployment.
* It offered a clear separation between content, theme, and build logic.

After exploring various options, Hugo caught my attention for it being newer and faster to build pages.

I settled on using the [anatole theme](https://themes.gohugo.io/themes/anatole/) for its minimalist yet appealing design. While the focus was on content, I appreciated the theme's stylish layout. Nevertheless, I aimed to personalize it—adjusting the layout, image display, and more. These modifications proved to be the most challenging aspect, involving numerous deployments for minor tweaks and reacquainting myself with CSS, HTML, and templating. Despite my somewhat outdated web design skills, I was pleased with the resulting Hugo site adorned with the Anatole theme. The result of this initial site can be seen below.

![Old site](/img/2020-12-11-runecaster/avcon.jpg)

# Site Revamp

After some initial activity, the blog lay dormant. Fast forward to 2024, the urge to share new work prompted me to revisit the site. Previously, I had used the CMS Forestry for professional projects, only to discover it had evolved into Tina. Upon updating Hugo and attempting a deployment, I encountered issues due to my theme's incompatibility with the latest Hugo version. My theme, a fork of the original, seemed too outdated. Attempting to update it proved futile due to the extensive changes required. I opted to adopt the latest theme version, painstakingly transferring my customizations. This transition was particularly challenging as the theme had adopted SCSS—a precompiled CSS that I was unfamiliar with but eventually found to align well with static site generation. Despite the steep learning curve, I managed to integrate most of my original modifications, adapting some to my changed preferences. A comparison of the code changes is available here.
Infrastructure Update

A significant benefit of the Hugo update was the modernization of my deployment infrastructure. Previously reliant on a cumbersome setup involving three repositories, the new framework streamlined to two, with a GitHub Action facilitating CI/CD deployment to GitHub Pages.

```
Content Repository
│
├── Hugo Content
├── Go Module: Theme Repository
│   └── Hugo Theme
│
└── GitHub Actions
    └── Deploy to GitHub Pages
```

This new setup not only simplified the deployment process but also subtly enhanced the site's aesthetics, thanks to Hugo's robust content separation framework. Adapting to the theme's modularization, however, presented new challenges due to its external repository management. This complexity was mitigated by referencing the theme's branch instead of specific commits, although this workaround had its limitations, particularly with local server previews reverting to the latest commit. Despite these hurdles, the site's evolution has reinvigorated my enthusiasm for blogging, setting the stage for new content creation.

```
Content Repository
│
├── Hugo Content
├── Go Module: Theme Repository
│ └── Hugo Theme
│
└── GitHub Actions
└── Deploy to GitHub Pages
```

# Looking Forward

There's a few changes I'd like to integrate in the future

* Add comments to posts
* Add the ability to share posts
* Add a portfolio section (the anatole theme now supports this)

After navigating these updates, I'm now poised to concentrate on producing the blog posts that initially inspired this venture, despite my propensity for distraction.