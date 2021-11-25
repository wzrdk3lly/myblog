---
title: "Starting a Blog with Hugo and Github for Free"
date: 2021-11-24
tags: ["#alpha", "#git", "#Jobs"]
showAuthor: true
showDate: true
---

This article explains why I started a blog and how you can too. I'm going to show you step by step how to create a simple blog with Hugo and Github for FREE. 

## Why I Started a Blog

My life is in shambles after the never ending rug pulls....lol I'm completely joking. Long story short, I created this blog to:
- help other beginners in infosec and web3
- solidify my knowledge of concepts through teaching and writing 
- present my knowledge to future employers/clients

For the sake of time, I’m going to spare you my detailed reasons. Be on the lookout for future posts explaining the benefits of starting a blog from a beginners point of view. 

## How to create a blog with Hugo and Github pages

The first thing you should know is that it took me about a week to learn and create this blog. I knew the basics of git/github and that's about it. I struggled through what many technical people probably wouldn't. I stayed focused on the task at hand and stumbled my way to creating it. When you read my writeup you may not understand what's going on. It's okay. A week ago, I wouldn't either. Use the resources I list at the bottom of this post to help you when you get stuck. Okay...enough with the pep-talk. Let's get into this write up. 

Assuming you are using a linux OS, I'm going to walk you through the process of installing hugo and hosting your website on github.

### Steps

To install hugo, type the command `sudo snap install hugo`.

To initialize the blog, type the command `hugo new site [insert blog name]`.

Navigate to [Hugo's themes](https://themes.gohugo.io/) and choose one that you like. 

Within the root folder of your Hugo blog, type the command `git submodule add [insert link to theme] themes/[insert theme name]`.

Create a git branch with `git branch -M main`.

Create a github repository and name it the same thing that you named your hugo site. 

In your terminal type `git remote add origin [https://github.com/[insert username]/[insert blog name]`.

Then type `git push -u origin main`

You will know this was done successfully when you can see the repository in github.

Next, you will need to deploy your site to github pages.

Create a folder within your blog directory titled ".github".

Within the ".github” folder, create a subdirectory titled "workflows"

Within the "workflows" folder create a file titled "gh-pages.yaml"

Copy and paste the following code into the yaml file:

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

You will know this is done successfully when you have a branch titled "gh-pages".

Navigate to Settings > Pages and then copy your github URL into your clipboard.

Edit your blog's “config.toml” file with your github URL.

Push your updated files to github and your link should now be live! 

### Resources
- [Hugo Documentation](https://gohugo.io/documentation/)
- [Helpful Youtube Tutorial](https://www.youtube.com/watch?v=psyz4UPnGAA&ab_channel=CodeNanshu)





