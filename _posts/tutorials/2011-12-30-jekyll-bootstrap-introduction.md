---
layout: post
title: "Jekyll Bootstrap Introduction"
description: ""
category: tutorial
tags: [jekyll, bootstrap, tutorial]
---
{% include JB/setup %}

Read [Jekyll Quick Start](http://jekyllbootstrap.com/usage/jekyll-quick-start.html)

Complete usage and documentation available at: [Jekyll Bootstrap](http://jekyllbootstrap.com)

## Configurations

In `_config.yml` remember to specify your own data:

    title : My Blog =)

    author :
      name : Name Lastname
      email : blah@email.test
      github : username
      twitter : username

    links :
      - href : http://mcspring.github.com
        title : Memento of Spring
        tagline : personal write

The theme should reference these variables whenever needed.

## Create a Post

You can create a new post easily via rake task:

    $ rake post title="Jekyll Bootstrap Introduction"

The rake task automatically creates a file with properly formatted filename and YAML Front Matter. Make sure to specify your own title use `title="You New Post Title"`. By default, the date is the current date.

The rake task will never overwrite existing posts unless you tell it to.

## Create a Page

You can create a new page easily via rake task:

    $ rake page name="about.md"

or create a nested page:

    $ rake page name="pages/about.md"

or create a page with a "pretty" path:

    # this will create the file: ./pages/about/index.html
    $ rake page name="pages/about"

The rake task automatically creates a page file with properly formatted filename and YAML Front Matter as well as includes the Jekyll Bootstrap “setup” file.

## Publish

After you’ve added posts or made changes to your theme or other files, simply commit them to your git repo and push the commits up to GitHub.

    $ git add .
    $ git commit -m "new post: Jekyll Bootstrap Introduction"
    $ git push origin master

A GitHub post-commit hook will automatically deploy your changes to your hosted blog. You will receive a success or failure notice for every commit you make to your blog.

## To-Do

This theme is still unfinished. If you'd like to be added as a contributor, [please fork](http://github.com/plusjade/jekyll-bootstrap)!
We need to clean up the themes, make theme usage guides with theme-specific markup examples.

