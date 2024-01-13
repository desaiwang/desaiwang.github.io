---
title: "Hexagons, external libraries, and multiple files"
date: 2024-01-11T13:07:06-05:00
draft: false
tags: ["tutorial", "p5js"]
showtoc: true
---

I've been feeling stuck recently. The initial excitement has faded, and I realized that what I can achieve in my sketches is far less than what I had imagined. Writing new code for each sketch is a lot of work, and when things don't go expected, debugging is even more painful.

I feel defeated, and I question my initial reason for pursuing computational art. I wanted to find joy through art, but was I just romanticizing art-making? If anything, trying to make art with code has been frustrating and makes me feel like I suck at both coding and art. Maybe this means I am stepping outside of my comfort zone? Maybe this is a good thing, as failure is the harbinger of success? I don't know. Anyways, this is a chronicle of a goose chase related to hexagons.

The Genuary 10 prompt was *hexagonal*, and I found the [linked article](https://www.redblobgames.com/grids/hexagons/) from Red Blob Games super interesting. Geometric properties, axial coordinates, common algorithms... The information appeared like documentation to a computer science course project, and I was eager to get started implementing my own hexagon library. However, I quickly realized such is no simple task, and if anything, it takes away from my main goal of making art.

Why invent the wheel? I should just use an existing library! [Honeycomb](https://abbekeultjes.nl/honeycomb/guide/getting-started.html) is a Javascript library that seems to fit my needs, but wait... how do I incorporate it into p5.js sketch? This seems easy, but took me forever to figure out. You just need to add the library to the `head` section of your html file (if you are using the p5.js web editor, this is `index.html`):
```
<script src="https://unpkg.com/honeycomb-grid@4.1.5/dist/honeycomb-grid.umd.js"></script>
```
And then now you can use any function from this library by calling `Honeycomb.<function>`.

### CDN vs Local
Notice that the source I used for the Honeycomb library is a web address, and not a local address. This reflects the usage of a [Content Delivery Network](https://aws.amazon.com/what-is/cdn/) (CDN), as opposed to downloading the library to my computer and referencing it locally. The main difference is that CDN speeds up page loading time by delivering the user files from a nearby physical location. They are also optimized for static content management, and will result in better web performance when there are a lot of users and requests. However, one downside is that using CDN makes your website dependent on other servers, which can change and break.

Performance is not an issue when creating a simple sketch, but I used a CDN because I think it's easier than downloading the library and uploading it to the p5.js online editor.

### hexagonal fireworks
{{<240111-Genuary10-hexagons>}}

Code [here](https://editor.p5js.org/desaiwang/sketches/jPGhfqVlE).

I wanted to create a firework effect that radiates outwards from the central hexagon. I followed the Honeycomb documentation on ring traversals and colored the ring at a certain radius (a mod function on frameCount, so the radius would increase then go back to 0). Then I made the center coordinates into variables, and registered some key input events that allowed the center to move. Lastly, I wanted to capture the delay of fireworks--that is, the old centers should still radiate outwards, but at a diminished opacity. I created an array which stores the most recent 5 center locations. Lastly, I made a mapping from the position of a center in the center list to opacity, and colored its ring accordingly.

I found the hexagonal sizes a bit difficult to set correctly (xRadius and yRadius don't correspond directly to a cartesian grid), so I set the canvas size to 400*400 and manually adjusted the number of tiles in the x and y directions. I want to explore hexagonal coordinates a bit more in depth: What determines if a grid coordinate is negative? Why is it not symmetrical? 

### multiple .js files
Looking through other creator's Genuary code, I found that they often have multiple .js files. This can be very helpful for organization, and for keeping the main sketch.js as simple as possible. To include other .js files (for example colorscheme.js) add the following code to the `body` section of the html file:

```
<script src="colorscheme.js"></script>
```

I noticed that many creators include a color scheme file, which has list of color in hex code. I wanted to visualize the hex codes, so I created a simple sketch that displays the scheme name and color. Pressing any key will shuffle the scheme. I also allows users to search for a specific theme by uncommenting the `setPalette = ` on line 25 in sketch.js. You can try toggling between the different schemes in the sketch below, but refer to the [online editor](https://editor.p5js.org/desaiwang/sketches/oxejCRTXV) if you want to play around with setting a palette.

{{<240111-palette>}}