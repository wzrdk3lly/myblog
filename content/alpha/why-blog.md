---
title: "Free Alpha: Start a Blog"
date: 2021-11-23
tags: ["blog alpha", "git/git hub", "job hunting"]
---

This article explains why I started a blog and how you can too. I'm going to walk you step by step on how to create a simple blog for Free. 

## Why I stared a blog

My life is in shambles after the never ending rug pulls....lol I'm completely joking. Long story short, I created this blog for three reasons:
- help other beginners in infosec and web3
- better understand concpets through teaching and writing 
- present to future employers/clients my technical skills

While I could further elaborate on those three topics, I won't for the sake of time. We can talk more about the "why" via twitter [@wzrdk3lly](https://twitter.com/wzrdk3lly).

## How to create a blog with Hugo and Github pages

The first thing you should know is that it took me about a week to learn and create this blog. I knew the basics of git/github and that's about it. I struggled through what many who are technical probably wouldn't. I stayed focused on the task at hand and stumbled my way to somehow creating this post. As a beginner, you will face this alot with any new project/task you encounter. When you read my writeup you may not understand what's going on. It's okay, a week ago, I wouldn't either. Use your trusty google search and youtube university and you will get it eventually. Okay enough with the pep-talk. Let's get into this technical write up. 

Assuming you are using a linux OS, I'm going to walk you through the process of installing hugo and hosting your website on github.

### Steps

Run the command `sudo snap install hugo` to install hugo.

Run the command `hugo new site [insert blog name]` to create your new site.

Navigate to [Hugo's themes](https://themes.gohugo.io/) and choose one that you like. 

Within the root folder of your Hugo blog, type the command 'git submodule add [theme git hub link] themes/[theme name]'

create a git branch with `git branch -M main`

Create a github repository and name it the same thing that you named your hugo site. 

In your terminal type `git remote add origin [https://github.com/username/newblog]`

Then type `git push -u origin main`

You will know this was done successfully when you can see the repository in github

Next, you will need to deploy your site to github pages.

create a folder within your blog directory titled ".github".

Within the ".github folder" create a subdirectory titled "workflows"

Withing the "workflows" folder create a file titled "gh-pages.yaml"

copy and paste this code into the yaml file:

```
name: github pages

on:
  push:
    branches:
      - main  # Set a branch to deploy
  pull_request:

jobs:
  deploy:
    runs-on: ubuntu-20.04
    steps:
      - uses: actions/checkout@v2
        with:
          submodules: true  # Fetch Hugo themes (true OR recursive)
          fetch-depth: 0    # Fetch all history for .GitInfo and .Lastmod

      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: 'latest'
          # extended: true

      - name: Build
        run: hugo --minify

      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        if: github.ref == 'refs/heads/main'
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
```

push your repository to github with the following commands:

```
git add .
git commit -m "deploy"
git push 

```

You will know this is done succesffuly when you have a branch titled "gh-pages"

Navigate to Settings > Pages and then copy your github URL into your clipboard

Edit your blog's config.toml file with your github URL

Push your updated files to github and your link should now be live! 







