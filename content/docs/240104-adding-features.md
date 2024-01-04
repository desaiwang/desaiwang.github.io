---
title: "Adding Features in Hugo Blog"
date: 2024-01-04T10:01:47-05:00
draft: false
tags: ["hugo", "webdevelopment", "tutorial"]
showtoc: true
---

### Adding Features
The [sample PaperMod page](https://adityatelange.github.io/hugo-PaperMod/) has many features, like a page intro, and a menu on the top right. 
![Sample PaperMod landing page](/images/240104-adding-features/sample_menu.png)
These are not included by default, so let's talk about how to configure them. The manipulations will be mostly based in hugo.yaml, with the addition of some files in the layout structure. I omit many possible features (toggle for multiple languages, different modes, navigation aids), but for those you can refer to the [example site](https://github.com/adityatelange/hugo-PaperMod/tree/exampleSite)'s config.yml, or read more about PaperMod on their [website](https://adityatelange.github.io/hugo-PaperMod/) and [wiki](https://github.com/adityatelange/hugo-PaperMod/wiki/Features).


### Website Intro
To have a intro on your landing page, follow this template and add it at the end of your hugo.yaml:
```
params:
  author: Desai Wang
  homeInfoParams:
    Title: "art + computation"
    Content: >
      Welcome to my digital sketchbook 🎉
      

  socialIcons:
    - name: Github
      url: "https://github.com/desaiwang"
    - name: LinkedIn
      url: "https://www.linkedin.com/in/desaiwang/"
    - name: Portfolio
      url: "https://desaiwang.com"
```

Spacing matters, so make sure everything is indented inside params. And params should be at the outermost level. You can also add other icons such as Youtube or X.
I noticed that the spacing on mine 

### Site Configurations
There are some site-wide configurations that I wanted to apply, such as enabling emojis, displaying a table of contents at the top of each blog page, adding sharing options at the bottom of blog pages. Add these inside the param block we just created (indent should match those of author, homeInfoParams, and socialIcons).

```
  # ShowReadingTime: true
  ShowShareButtons: true
  ShareButtons: ["linkedin", "x", "reddit"] # customize which share buttons to be enabled on page by editing this list
  ShowToc: true   #table of content at top of each page
  defaultTheme: auto
```

You can also chose to override these setting for each individual page by adding variables to the front matter. Refer to the [documentation](https://adityatelange.github.io/hugo-PaperMod/posts/papermod/papermod-variables/) for more information.

If you want to enable emojis, add `enableEmoji: true` at the outermost level in hugo.yaml (not in params).

### Menu bar
For my menu, I wanted an timeline archive, search function, tags, and a link to my personal website.

First add a menu section at the end of your config file, hugo.yaml:
```
menu:
  main:
    - name: Archives
      url: archives
      weight: 5
    - name: Tags
      url: tags/
      weight: 10
    - name: Search
      url: search/
      weight: 15
    - name: "& more"
      url: https://desaiwang.com/
```
The lower the weight number, the more left it will be when ordered. Those without weights will be at the end. The simple &more link should be working, but the rest needs some additional structure which we will now set up. 

#### archive timeline
Create archives.md inside the content folder.
```
.
├── hugo.yaml
├── content/
│   ├── archives.md   <--- Create archive.md here
│   └── posts/
├── static/
└── themes/
    └── PaperMod/
```

Add the following to archives.md:
```
---
title: "Archives"
layout: "archives"
url: "/archives/"
summary: archives
---
```

#### tags
You don't have to create any additional structure. You can add tags to posts via their front matter using the variable `tags`. For example, this article has:
```
---
title: "Adding Features in Hugo Blog"
date: 2024-01-04T10:01:47-05:00
draft: false
tags: ["hugo", "tutorial-web"] #example with two tags
showtoc: true
---
```

#### search
To enable search, first add this section to hugo.yaml, before params:

```
outputs:
  home:
    - HTML
    - RSS
    - JSON # necessary for search
```
Then add search.md inside the content folder, and add the following to the file:
```
---
title: "Search" # in any language you want
layout: "search" # necessary for search
summary: "search"
placeholder: "search site"
---
```

You can hide a page from showing up through search by adding `searchHidden: true` to its front matter. To read more about possible customizations, refer to the last section of the [official documentation](https://adityatelange.github.io/hugo-PaperMod/posts/papermod/papermod-features/#search-page).

Now you should have a functioning menu!

### Additional Manipulations

#### adjust introduction container height
I noticed that even though my introduction is short, the container height for the introduction doesn't adjust. This is because there is a minimum height set in themes\paperMod\assets\css\common\post-entry.css, on line 6.

```css {linenos=true}
.first-entry {
  position: relative;
  display: flex;
  flex-direction: column;
  justify-content: center;
  min-height: 320px;
  margin: var(--gap) 0 calc(var(--gap) * 2) 0;
}
```
To overwrite the default settings, create assets\css\common\post-entry.css in your root directory, and copy the content of the original file. Change line 6 to a height that you like, for me, this was 200px.  

320px Height          |  200px Height
:-------------------------:|:-------------------------:
![320px float container height](/images/240104-adding-features/my_blog_spacing.png)  |  ![200px float container height](/images/240104-adding-features/my_blog_spacing_200.png)


#### update default post
Since now there's more functionality, I updated the post template, which is archetypes/default.md. This is what is included when you create a post with command `hugo new docs/<post_name>.md`.
```
---
title: "{{ replace .File.ContentBaseName "-" " " | title }}"
date: {{ .Date }}
draft: true
tags: ["tutorial-web", "p5.js"]
showtoc: true
---
```

### Closing Thoughts
Phew! My digital sketchbook has finally come together! It would be great to have commenting features and a site logo, but for now, it's time to add some p5.js sketches/doodles!
