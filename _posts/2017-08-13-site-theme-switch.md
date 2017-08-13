---
layout: post
title: Site Theme Switch
date: 2017-08-13 12:48:00 -0500
comments: true
tags: jekyll-theme jekyll bootstrap
---

**Just a quick note to anyone who stumbles across the git history of this site.**

When I first started this blog I used the [slate](https://github.com/pages-themes/slate) theme since it was suppored by github pages. Out of the box this is great since it gave a clean interface with basically zero work; however, making even simple changes required a lot more work than I thought they should. 

The current iteration of Jekyll obscures a lot of what's happening with the themes and overriding styles required basically pulling down the git repo of the theme, including the various layouts and styles, and then making the tweaks I desired. 

I was not a fan of this, so I refactored most of the styling to use [bootstrap](https://getbootstrap.com/) instead. The look of the site is virtually unchanged, but my piece of mind is much improved. 