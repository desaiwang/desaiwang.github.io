---
title: 'Creating a blog with hugo'
date: 2024-01-03T13:17:00-05:00
draft: true
---

## Choosing a framework
I worked with basic html and css for a data-visualization course, but most of the projects were about displaying json using the d3 library. That said, I had no experience of creating a nice-ish looking website with multiple pages when I set off to create my digital sketchbook.

Solution criteria:
1. able to include p5.js (most important, as this is the reason I abandoned [my wix blog](desaiwang/blog))
2. can be hosted on github.io (free domain)
3. easy to create

I've heard of React, but from a quick search it seems like a development framework, which means I would be coding a blog from scratch. What I want instead is an existing template that I can modify, so I turned to static site generators. They parse plain text (technically [markdown](https://www.markdownguide.org/getting-started/), which has more formatting functionality) into webpages, and have fast performances. But which one should you use: Jekyll, Hugo, Zola, Gatsby...? Each one is based in a different programming language, but I think they are all very similar except for different available themes. I first went with Zola because it automatically parses javascript in markdown and makes it a bit easier to include p5.js code compared to the other frameworks, which require the code to be saved in a separate file and then referenced in the markdown. However, halfway into writing my first post I realized that the blog theme I chose didn't have a search bar, and couldn't find another Zola theme that I liked. I ultimately decided to use the [PaperMod](https://adityatelange.github.io/hugo-PaperMod/) theme inside [Hugo](https://gohugo.io/).


## Creating a blog with Hugo
I followed the [PaperMod](https://adityatelange.github.io/hugo-PaperMod/posts/papermod/papermod-installation/) and [Hugo](https://gohugo.io/getting-started/quick-start/) documentation. There are some differences between the two instructions that can be confusing, especially if you're unfamiliar with hugo. Here are the steps I used to create my blog. I have a windows system, so if you use macOS or Linux you should refer to the official documentation instead.

1. Install [PowerShell](https://learn.microsoft.com/en-us/powershell/scripting/install/installing-powershell-on-windows?view=powershell-7.4). This is different from Windows PowerShell, and recommended by hugo.



The most common one is Jekyll, but I didn't find any themes I like.

and after consulting some cs friends I settled on using a prexiI asked my


I have no web-design experience, and was absolutely lost when I set off to create a website for myself.
This is **bold** text, and this is *emphasized* text.

Visit the [Hugo](https://gohugo.io) website!


{{< sketch1 >}}

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nunc eu feugiat sapien. Aenean ligula nunc, laoreet id sem in, interdum bibendum felis. Donec vel dui neque. Praesent ac sem ut justo volutpat rutrum a imperdiet tellus. Nam lobortis massa non hendrerit hendrerit. Vivamus porttitor dignissim turpis, eget aliquam urna tincidunt non. Aliquam et fringilla turpis. Nullam eros est, eleifend in ornare sed, hendrerit eget est. Aliquam tellus felis, suscipit vitae ex vel, fringilla tempus massa. Nulla facilisi. Pellentesque lobortis consequat lectus. Maecenas ac libero elit.
<!-- more -->
Ut luctus dolor ut tortor hendrerit, sed _hendrerit augue scelerisque_. Suspendisse quis sodales dui, at tempus ante. Nulla at tempor metus. Aliquam vitae rutrum diam. __Curabitur iaculis massa dui__, quis varius nulla finibus a. Praesent eu blandit justo. Suspendisse pharetra, arcu in rhoncus rutrum, magna magna viverra erat, eget vestibulum enim tellus id dui. Nunc vel dui et arcu posuere maximus. Mauris quam quam, bibendum sed libero nec, tempus hendrerit arcu. Suspendisse sed gravida orci. Fusce tempor arcu ac est ___pretium porttitor___. Aenean consequat risus venenatis sem aliquam, at sollicitudin nulla semper. Aenean bibendum cursus hendrerit. Nulla congue urna nec finibus bibendum. Donec porta tincidunt ligula non ultricies.

- Itemize 1
- Itemize 2
- Itemize 3

1. Enumeration 1
2. Enumeration 2
3. Enumeration 3

Sed vulputate tristique elit, eget pharetra elit sodales sed. Proin dignissim ipsum lorem, at porta eros malesuada sed. Proin tristique eros eu quam ornare, suscipit luctus mauris lobortis. Phasellus ut placerat enim. Donec egestas faucibus maximus. Nam quis efficitur eros. Cras tincidunt, lacus ac pretium porta, dui dolor varius elit, eget laoreet justo justo vitae metus. Morbi eget nisi ut ex scelerisque lobortis ut in lorem. Vestibulum et lorem quis ipsum feugiat varius. Mauris nec nulla viverra nisi porttitor efficitur. Morbi vel purus eleifend, finibus erat non, placerat ipsum. Mauris et augue vel nisi volutpat aliquam. Curabitur malesuada tortor est, at condimentum neque eleifend in.

