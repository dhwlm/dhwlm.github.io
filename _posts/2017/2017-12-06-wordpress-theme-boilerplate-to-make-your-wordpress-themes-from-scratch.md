---
layout: "post"
title: "Wordpress theme boilerplate to make your wordpress themes from scratch"
description: "As Web Developers our main goal is to do as little work as possible. "
date: "2017-12-06 17:57"
tags: [wordpress, theme, boilerplate ]
image:
  feature: wordpress-boilerplate-theme.jpg
  path: /images/wordpress-boilerplate-theme.jpg
---

# Wordpress Theme Boilerplate

I found myself writing the same starter wordpress theme time and time again, so I decided to create this simple boilerplate to help reduce the time required when starting a new wordpress theme. This will give you the basic files and structure of the theme.

## Installing / Getting started

Download/clone the boilerplate theme from my [github repo](https://github.com/dhwlm/wordpress-theme-boilerplate){:target="_blank"}

```shell
git clone https://github.com/dhwlm/wordpress-theme-boilerplate.git your-theme-name
```

This will create a folder with 'your-theme-name' and the boilerplate files inside it. You can then choose this theme from the wordpress admin panel.

## Content

### Folder Structure

```shell
|-assets
  |-css
    |-admin.css
    |-theme.css
|-inc
  |-customizer
    |-logo-customizer.php
  |-limit-login-attempts.php
  |-rebranding.php
  |-remove-junk.php
|-footer.php
|-functions.php
|-header.php
|-index.php
|-README.md
|-single.php
|-style.css
```

### File Usage/Explaination

**admin.css**: write admin panel/login screen specific css

**theme.css**: this file contains basic 12 grid layout by bootstrap and some classes like text-center, clearfix, xs,ms,md,lg-hidden etc

**logo-customizer.php**: adds option in wordpress customizer to upload logo

**limit-login-attempts.php**: limits login attempts after 3 failed logins and blocks the user for 5mins. Time can be changed in this file.

**rebranding.php**: contains code to rebrand the admin panel and include admin.css

**remove-junk.php**: removes junk css, js etc files which wordpress adds by default. Also removes jquery migrate and disable admin bar on the frontpage when logged in

**style.css**: contains basic css and reset and global elements styles eg. .btn etc


### Post Installing

Certain Folders & files that are required are theme specific.
Please follow this checklist to complete the basic theme folder

  * Add/include *screenshot.png* inside the theme folder (this will give the preview of the theme in the admin panel)
  * Create **template-parts/** folder (add all the reusable template parts inside this folder)
  * Create **page-templates/** folder (add all the page templates inside this folder)
  * Create **img/** folder inside assets folder which will contain **layout/** & **content/** as subfolder
    - add layout specific images to layout folder & content specific images to content Folder
    - use css *background-image* property for layout specific images
    - use `<img src>` tag for content specific images
  * Remaining js, fonts, etc folders should be created inside **assets/** folder
  * Any functional php files should be added inside **inc/** folder. If need be, use subfolders to organize files related to specific functions
    - eg: widgets related files should all go inside **inc/widgets** with file name -> *footer-widget.php*
  * Keep your *functions.php* file clean by using includes


## About the Author

This Wordpress Theme boilerplate is created and maintained by [Dhawal Mehta](http://dhawalmehta.com).

### Disclaimer

This Wordpress Theme boilerplate has been made taking in consideration my personal usage and also it is in active development. I would appreciate any suggestions that will help me to enhance this project.

## Licensing

[MIT license](https://dhawal.mit-license.org/){:target="_blank"}
