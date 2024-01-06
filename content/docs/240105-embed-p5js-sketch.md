---
title: "Embedding P5.js Sketch and Genuary Challenge"
date: 2024-01-04T12:12:11-05:00
draft: false
tags: ["hugo", "tutorial-web", "p5js", "genuary"]
showtoc: true
---

### Embedding P5.js 
You can add javascript code in .md files by putting them inside an .html files at `layouts/shortcodes`. 
I first attempted putting p5.js code directly inside a `<script>` tag inside my .html file, but the visualizations would render at the bottom of the blog page. Further, additional elements did not conform with the rest of the page, you can see that the slider is at the very left corner.

![Alt text](/images/240105-embed-p5js-sketch/p5js-non-conform.png)


So, instead of adding code, I just saved my script to the p5.js [online editor](https://editor.p5js.org/) and embedded it with an `iframe` element. For example, for my first sketch I followed the Coding Train's [tutorial](https://www.youtube.com/watch?v=1h6vZl-OuB0) and created a starfield simulation. (Albeit a great intro, I think the online editor is actually just as easy to use as Visual Studio Code!) 


{{< sketch1 >}}


To display it here, I created `layouts/shortcodes/sketch1.html`. Inside, it just includes an iframe element with the src as the share link from the online editor:

```
<iframe style="border: 0px; width: 500px; height: 500px;"
  src="https://editor.p5js.org/desaiwang/full/9TGN5zpUO"></iframe>
```

And in my .md file for this post, I referenced it as ```{.{.<.sketch1.>}.}.``` (remove all the periods, I couldn't display it without hugo parsing it otherwise).
Super easy integration! However, I noticed that the editor function breaks the element. And I don't know how to center it. I have these on my to-investigate list.

### Genuary 05
I discovered the [Genuary](https://genuary.art/prompts) challenge today, and decided to join in. Today's prompt was on [Vera Molnar](https://www.sothebys.com/en/articles/vera-molnar-the-grande-dame-of-generative-art), and I found her work extremely inspiring. Here is my attempt to capture the spirit of her 1969 work titled *Interruptions*. 

{{< 240105-Genuary5-VeraMolnar >}}

I'm still grasping the intricacy of P5.js, so this submission was created by re-mixing some concepts presented by the book [Generative Design](http://www.generative-gestaltung.de/2/). You can also checkout other submissions on this [virtual gallery](https://www.joyn.xyz/contest/genuary-day-gallery-in-the-style-of-vera-moln-r--62362fbf8822?)

