---
title: "Updating This Blog: Hugo and Theme"
date: 2024-02-01T01:43:59+09:30
Tags: ['hugo','blog','scss','github','cicd']
---

* [Content Repo](https://www.youtube.com/watch?v=L0nRFNWD4p8)
* [My Anatole Fork Repo](https://github.com/Rhiyo/runecaster-java)
* [Anatole Theme](https://github.com/Rhiyo/runecaster-java)

thisisthestartofsummary

# Foundation of this Blog

This post outlines the journey of updating my blog, a story I realized I've never shared—the original construction of this site. Embarking on this project was more daunting than anticipated, encompassing both the initial setup and the subsequent updates. Thus, detailing this experience seemed necessary.

In 2020, amidst job searching, I sought a digital space to display and discuss my projects—a hybrid of a portfolio and a blog. This space was intended for tutorials, updates on my endeavors, or any topic of interest, essentially an "everything blog."

While I could have opted for any blogging platform, my path led me to static site generators, striking the perfect balance:

* Code customization was possible.
* It allowed for self-hosting.
* The site was fast, generated at deployment.
* It offered a clear separation between content, theme, and build logic.

After exploring various options, [Hugo](https://gohugo.io/) caught my attention for it being newer and faster to build pages.

I settled on using the [anatole theme](https://themes.gohugo.io/themes/anatole/) for its minimalist yet appealing design. While the focus was on content, I appreciated the theme's stylish layout. Nevertheless, I aimed to personalize it—adjusting the layout, image display, and more. These modifications proved to be the most challenging aspect, involving numerous deployments for minor tweaks and reacquainting myself with CSS, HTML, and templating. Despite my somewhat outdated web design skills, I was pleased with the resulting Hugo site adorned with the Anatole theme. The result of this initial site can be seen below.

![Old site](/img/post/2024-02-01-updating-this-blog-hugo-and-theme/old-custom-theme.png)

# Site Revamp

After some initial activity, the blog lay dormant. Fast forward to 2024, the urge to share new work prompted me to revisit the site. Previously, I had used the CMS Forestry for professional projects, only to discover it had evolved into Tina. Upon updating Hugo and attempting a deployment, I encountered issues due to my theme's incompatibility with the latest Hugo version. My theme, a fork of the original, seemed too outdated. Attempting to update it proved futile due to the extensive changes required. I opted to adopt the latest theme version, painstakingly transferring my customizations. This transition was particularly challenging as the theme had adopted SCSS—a precompiled CSS that I was unfamiliar with, but with the help of ChatGPT, I was able to navigate it. I found that SCSS aligned well static site generation as they both precompile. Despite the steep learning curve, I managed to integrate most of my original modifications, adapting some to my changed preferences. A comparison of the code changes is available [here](https://github.com/Rhiyo/anatole/compare/9f9e0f4..2cf7bb4).

A high level list of changes were:
* Switch post thumb nails to appear in a small box on the left on the home page
* a slightly bigger box on the right when on a single page
* Removed the border between the sidebar and main content
* Changed tags and date to appear above post preview, changed tags to have a box style
* Move read more to bottom right
* Many tweaks to the sizing and alightments of elements, espcially on the post lists and post themselves.

# Bug in original theme code

I'd found what I thought to be an bug in the theme code as well. On the homepage, the sidebar title was wrapped in a h3 tag. However outside of the homepage it was wrapped in a div. I assume this is for SEO reasons. Although they had the same styling class, the margin was set to 1em and this was somehow being computed differently for the two different tags. 24px for h3, and 16 for a div. Causing the content above and below the title to be farther away while on the homepage. Although a small issue, this irked me. I fixed by keeping a styled div regardless of the page and adding a h3 tag within the div when it's the homepage only, styling the h3 tag within this div to not have any margin. I made a [PR for this fix](https://github.com/lxndrblz/anatole/pull/487) on the original theme as well, however it looks like the maintainer hasn't looked at PRs for a while.

# Updating Deployment Infrastructure

A significant benefit of the Hugo update was the modernization of my deployment infrastructure. Previously reliant on a cumbersome setup involving three repositories, the new framework streamlined to two, with a GitHub Action facilitating CI/CD deployment to GitHub Pages. The overview of the old deployment is below.

```
Content Repository
│
├── Hugo Content
├── Local Shell Script
│ ├── Commit/Push Changes
│ ├── Build Website
│ └── Manage Submodules
│
├── Submodule: Theme Repository (Fork)
│ └── Custom Theme Changes
│
└── Submodule: Deployed Code Repository (GitHub Pages)
├── Built Website Code
└── Deploys to GitHub Pages from Base Branch
```

The new setup not only simplified the deployment process but also subtly enhanced the site's aesthetics, thanks to Hugo's robust content separation framework. Adapting to the theme's modularization, however, presented new challenges due to its external repository management. This complexity was mitigated by referencing the theme's branch instead of specific commits, although this workaround had its limitations, particularly with local server previews reverting to the latest commit. A overview of the new structure is below and as you can see, is simplified.

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

All in all I like the changes I made to the new Anatole theme - a screenshot of which can be seen below.

![Default anatole](/img/post/2024-02-01-updating-this-blog-hugo-and-theme/current-default-theme.png)

Although the default theme is still great, I really wanted to just make something of my own.

There's a few changes I'd like to integrate in the future:

* Add comments to posts
* Add the ability to share posts
* Add a portfolio section (the anatole theme now supports this)

Now that I've revamped this blog - I can now get posting to not posting any other blog posts!