---
title: 'Creating a blog with Hugo'
date: 2024-01-03T13:17:00-05:00
draft: false
---

### Choosing a framework
I worked with basic html and css for a data-visualization course, but most of the projects were about displaying json using the d3 library. That said, I had no experience of creating a nice-ish looking website with multiple pages when I set off to create my digital sketchbook.

Solution criteria:
1. able to include p5.js (most important, as this is the reason I abandoned [my wix blog](desaiwang.com/blog))
2. can be hosted on github.io (free domain)
3. easy to create

I've heard of React, but from a quick search it seems like a development framework, which means I would be coding a blog from scratch. What I want instead is an existing template that I can modify, so I turned to static site generators. They parse plain text (technically [markdown](https://www.markdownguide.org/getting-started/), which has more formatting functionality) into webpages, and have fast performances. But which one should you use: Jekyll, Hugo, Zola, Gatsby...? Each one is based in a different programming language, but I think they are all very similar except for different available themes. I first went with Zola because it automatically parses javascript in markdown and makes it a bit easier to include p5.js code compared to the other frameworks, which require the code to be saved in a separate file and then referenced in the markdown. However, halfway into writing my first post I realized that the blog theme I chose didn't have a search bar, and couldn't find another Zola theme that I liked. I ultimately decided to use the [PaperMod](https://adityatelange.github.io/hugo-PaperMod/) theme inside [Hugo](https://gohugo.io/).


### Creating a blog with Hugo + PaperMod
I followed the [PaperMod](https://adityatelange.github.io/hugo-PaperMod/posts/papermod/papermod-installation/) and [Hugo](https://gohugo.io/getting-started/quick-start/) documentation. There are some differences between the two instructions that can be confusing, especially if you're unfamiliar with hugo. Here are the steps I used to create my blog. I have a windows system, so if you use macOS or Linux you should refer to the official documentation. If you already have some of the packages installed, no need to re-install them as long as the versions are up-to-date.

1. Install [PowerShell](https://learn.microsoft.com/en-us/powershell/scripting/install/installing-powershell-on-windows?view=powershell-7.4). This is different from Windows PowerShell, and recommended by hugo.
2. Install [Hugo](https://gohugo.io/installation/)
3. Install [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)

Now open PowerShell, navigate to the parent directory where you want to create your website folder, and execute the following commands. Replace `<YourSiteName>` with your site name. I used the yaml configuration.

```powershell
hugo new site <YourSiteName> --format yaml
cd <YourSiteName>
git init
git submodule add --depth=1 https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod
git submodule update --init --recursive
```

Inside hugo.yaml, add `theme: PaperMod` at the end. You can also change title to reflect your website.

Create a new page with command `hugo new <filename>`. For example:
```powershell
hugo new docs/test.md
```
The draft status is set to true, which means it will not be published. You should change it to false. Feel free to add some text, and change the title.

To build the website locally, run `hugo server` inside PowerShell. Run `hugo server -D` if you want to see drafts as well. Only move onto the next steps if your local host displays as expected.

### Publishing to GitHub 
I will discuss two ways of publishing to github, either directly to username.github.io, or to username.github.io/repository_name. If you want to host yours on a custom domain, follow the second approach, and then to refer to [this tutorial](https://theplaybook.dev/docs/deploy-hugo-to-github-pages/#link-custom-domain-to-github-pages). 

#### *username*.github.io
I don't have my personal website hosted on my main page, so I decided to host this sketchbook directly at desaiwang.github.io. 

To do this, first create a new public repository on Github named *username*.github.io, where *username* is your github username.

Then inside PowerShell, add a readme file, commit and make a branch named main:
```powershell
echo "# README" >> README.md
git add README.md
git commit -m "first commit"
git branch -M main
```
Then add the github repo you created as the remote origin. You can find the path of the github repo by clicking the green code button to the right on your github repo page and copying the HTTPS.:
```powershell
git remote add origin <path_to_your_git_repo>
git push -u origin main
```
Inside hugo.yaml, change the baseURL to that of your github pages, and also update the title. For example mine file contains:
```yaml
baseURL: "https://desaiwang.github.io"
languageCode: en-us
title: desai's doodles
theme: PaperMod
```

The default static website generator is jekyll, so we also need to add a .nojekll file at the root of this repository. You do not need to add any content to this file. 
Now follow the section on [building and deploying the site](#github-actions-for-building-and-deploying-site).

### *username*.github.io/project_repo
If you already have a personal page, and want to host a blog on sub-page, this approach is for you.

First create a new repository on Github and copy the path information.

Inside PowerShell, add a readme file, commit and make a branch named main:
```powershell
echo "# README" >> README.md
git add README.md
git commit -m "first commit"
git branch -M main

```
Then add the github repo you created as the remote origin. You can find the path of the github repo by clicking the green code button to the right on your github repo page and copying the HTTPS.:
```
git remote add origin <path_to_your_git_repo>
git push -u origin main
```

Inside hugo.yaml, change the baseURL to *username*.github.io/project_repo, and also update the title. Note that the project_repo must match the name of the repository you just created. For example, if my repository is named doodles, my yaml file should be:
```yaml
baseURL: "https://desaiwang.github.io/doodles"
languageCode: en-us
title: desai's doodles
theme: PaperMod
```

On the repository github page, go to Settings>Actions>General>Workflow permissions and set it to *Read and write permissions*.
Under Settings>Pages>Source, change it from *Deploy from a branch* to *GitHub Action*.

### GitHub Actions for building and deploying site
Lastly, we use github actions to build and deploy this website. Add a .github/workflows/deploy.yaml file (that is, an empty file named deploy.yaml at .github/workflows). Paste the content below into the file: 
```yaml
name: Deploy Hugo site to Pages

on:
  # Runs on pushes targeting the default branch
  push:
    branches:
      - main

  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

# Sets permissions of the GITHUB_TOKEN to allow deployment to GitHub Pages
permissions:
  contents: read
  pages: write
  id-token: write

# Allow only one concurrent deployment, skipping runs queued between the run in-progress and latest queued.
# However, do NOT cancel in-progress runs as we want to allow these production deployments to complete.
concurrency:
  group: "pages"
  cancel-in-progress: false

# Default to bash
defaults:
  run:
    shell: bash

jobs:
  # Build job
  build:
    runs-on: ubuntu-latest
    env:
      HUGO_VERSION: 0.121.0
    steps:
      - name: Install Hugo CLI
        run: |
          wget -O ${{ runner.temp }}/hugo.deb https://github.com/gohugoio/hugo/releases/download/v${HUGO_VERSION}/hugo_extended_${HUGO_VERSION}_linux-amd64.deb \
          && sudo dpkg -i ${{ runner.temp }}/hugo.deb          
      - name: Install Dart Sass
        run: sudo snap install dart-sass
      - name: Checkout
        uses: actions/checkout@v4
        with:
          submodules: recursive
          fetch-depth: 0
      - name: Setup Pages
        id: pages
        uses: actions/configure-pages@v4
      - name: Install Node.js dependencies
        run: "[[ -f package-lock.json || -f npm-shrinkwrap.json ]] && npm ci || true"
      - name: Build with Hugo
        env:
          # For maximum backward compatibility with Hugo modules
          HUGO_ENVIRONMENT: production
          HUGO_ENV: production
        run: |
          hugo \
            --gc \
            --minify \
            --baseURL "${{ steps.pages.outputs.base_url }}/"          
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v2
        with:
          path: ./public

  # Deployment job
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v3
```

Now commit the changes and push to github:
```powershell
git commit -a -m "add workflow"
git push origin main
```

You should see the actions showing up next to your commit message, first as a yellow dot. If they turn into green checks, that means everything was built and deployed successfully. You should be able to see your webpage at *username*.github.io/*project_repo*.

If not, read the error messages and see if you can decipher what went wrong. Asking the internet for help is a good idea, too. This took me a few tries (had an illegal apostrophe in my .md file name, found an extra / at the end of my baseURL, didn't have double quotes around my title for the yaml front matter, confused about whether or not I needed a gh-pages branch...), so don't be discouraged!

### Closing Thoughts
This took much longer than I thought it would, since I started with hosting my sketchbook at desaiwang.github.io/doodles and then transferred everything to desaiwang.github.io. Broke many things in the process and had to re-learn some git commands for bringing back past commits. Also, github actions are confusing, and the config files are a bit hard to work with. These I attribute to my general lack of experience working with web design, but I am beginning to sense some patterns in how things work.

In the next post, I add features to this site, such as the search bar that started this whole rabbit chase, along with a landing intro and tags.

