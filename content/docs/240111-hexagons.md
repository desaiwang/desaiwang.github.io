---
title: "Hexagons, external libraries, and multiple files"
date: 2024-01-11T13:07:06-05:00
draft: true
tags: ["tutorial", "p5js"]
showtoc: true
---


<!-- {{<240111-hexagons>}} -->
I've been feeling stuck recently. The initial excitement has faded, and I realized that what I can achieve in my sketches is far less than what I had imagined. Writing new code for each sketch is a lot of work, and when things don't go expected, debugging is even more painful.

I feel defeated, and I question my initial reason for pursuing computational art. I wanted to find joy through art, but was I just romanticizing art-making? If anything, trying to make art with code has been frustrating and makes me feel like I suck at both coding and art. Maybe this means I am stepping outside of my comfort zone? Maybe this is a good thing, as failure is the harbinger of success? I don't know. Anyways, this is a chronicle of a goose chase related to hexagons.

The Genuary 10 prompt was *hexagonal*, and I found the [linked article](https://www.redblobgames.com/grids/hexagons/) from Red Blob Games super interesting. Geometric properties, axial coordinates, common algorithms... The information appeared like documentation to a computer science course project, and I was eager to get started implementing my own hexagon library. However, I quickly realized such is no simple task, and if anything, it takes away from my main goal of making art.

Why invent the wheel? I should just use an existing library! [Honeycomb](https://abbekeultjes.nl/honeycomb/guide/getting-started.html) is a Javascript library that seems to fit my needs, but wait... how do I incorporate it into p5.js sketch? This seems easy, but took me forever to figure out. You just need to add the library to the `head` section of your html file (if you are using the p5.js web editor, this is `index.html`):
```
<script src="https://unpkg.com/honeycomb-grid@4.1.5/dist/honeycomb-grid.umd.js"></script>
```

### CDN vs Local
Notice that the source I included for Honeycomb is a web address, and not a local address. This reflects the usage of a [Content Delivery Network](https://aws.amazon.com/what-is/cdn/) (CDN), as opposed to downloading the library to my computer and referencing it locally. The main difference is that CDN speeds up page loading time by delivering the users files from a nearby physical location. They are also optimized for static content management, and will result in better web performance when there are a lot of users and requests. However, one downside is that using CDN makes your website dependent on other servers, which can change and break.

Performance is not an issue when creating a simple sketch, but I used a CDN because personally I think it's easier than downloading the library and uploading it to the p5.js online editor.

### multiple .js files


having multiple .js files in p5.js

understanding other people's code is perhaps the best way to learn
