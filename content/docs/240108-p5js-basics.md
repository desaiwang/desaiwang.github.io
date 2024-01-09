---
title: "P5.js Basics"
date: 2024-01-08T12:12:11-05:00
draft: false
tags: ["hugo", "tutorial", "p5js", "genuary"]
showtoc: true
---

I've created a few sketches for Genuary, and found p5.js quite intuitive. I want to briefly share the structure of p5.js sketches, and some simple logics I've been working with. I've been using *[Generative Design](http://www.generative-gestaltung.de/2/)* as a reference book in addition to the official p5.js documentation. The online repository contains lots of examples with source code, and I would definitely recommend checking it out if you are also learning p5.js!

### general layout and entry functions
p5.js follows the general rules of JavaScript (in terms of syntax and common data structures), but there are many functions unique to p5.js. `setup` and `draw` are the two I have interacted with the most so far. `setup` does exactly what its name suggests: it is executed prior to any drawing, so it's the place to create the canvas and set properties for drawings. `draw` will be executed many times each minute, and it should contain information about what and how things should be drawn. Here is a sample layout:
```javascript

//global variables (accessible in all functions)
var radius = 40;

function setup(){
  createCanvas(720,720);

  frameRate(10); //this sets the time the canvas will be redrawn each minute, the default is 60.
  
  //properties that's needed before drawing/ persistent properties
  noFill();
}

function draw(){
  ellipse(mouseX, mouseY, radius, radius); //p5.js can get location of mouseX and mouseY!
}
```

### drawing settings
The drawings settings persist until overwritten. If you want the same settings, then you should put them in `setup`. Otherwise, you can parametrically define settings (based on time, for example), inside the `drawing` function. Perhaps you'll find these useful:
```javascript
background();
fill();
stroke();
```

These 3 functions all take in a color, and are quite lenient with input format. For example, `background(0)` and `background(0,0,0)` both set the canvas as black. By default color is defined by values between 0 and 255 in the rgb model, but you can change the number domain and color mode by calling [`colorMode`](https://p5js.org/reference/#/p5/colorMode).

### shapes
Some simple geometry, refer to the p5.js [documentation](https://p5js.org/reference/) for arguments:
```javascript
ellipse()
circle()
line()
point()
rect()
```
You can also use Vertex functions to build a more complex polygon by connecting vertices. Here is an example based on a Generative Design [sketch](http://www.generative-gestaltung.de/2/sketches/?01_P/P_2_2_3_01):
```javascript

var formResolution = 10; //also the number of vertices for the shape
var radius = 100;
var angle;
var centerX;
var centerY;
var x =[];
var y =[];

function setup() {
  createCanvas(windowWidth, windowHeight);
  
  angle = radians(360 / formResolution);
  centerX = width / 2;
  centerY = height / 2;

  // init shape
  for (var i = 0; i < formResolution; i++) {
    x.push(cos(angle * i) * radius);
    y.push(sin(angle * i) * radius);
  }

  noFill();
  stroke(0, 50);
  strokeWeight(0.75);
  background(255);
  
  frameRate(10);
}

function draw(){
  beginShape();

  // first control point
  curveVertex(x[formResolution - 1] + centerX, y[formResolution - 1] + centerY);

  // only these points are drawn
  for (var i = 0; i < formResolution; i++) {
    curveVertex(x[i] + centerX, y[i] + centerY);
  }
  curveVertex(x[0] + centerX, y[0] + centerY);

  // end control point
  curveVertex(x[1] + centerX, y[1] + centerY);
  endShape();
}

```
### interactivity
Interactivity is something offered by generative art that is not present in traditional drawings and paintings. 

One way of incorporating interactivity is through user inputs. I think p5.js is great for this as it greatly simplifies the setup required to work with events. It's very easy to get mouse inputs and user actions. These might be of interest:
```javascript
mouseX //gets mouseX position
mouseY
pmouseX //mouseX position from previous frame, very useful for drawing lines/ having continuity
pmouseY
mouseIsPressed

key
keyIsPressed
```

### time and randomness
Another way to incorporate change is with time. `frameCount` is the most common way I've encountered of getting time, and you can convert it to seconds (not always necessary) by dividing by `frameRate`.

However, as `frameCount` strictly increases, it can be difficult to work with directly. That is, if you are drawing a circle and set the radius to be frameCount, this will blow up very quickly! Instead, some modulating function is required. Sine and cosine are very popular, as is a normal mod.

To be even a bit more ambitious, how about making the loops less monotonous by introducing some randomness into your cycles? Adding noise quite a common approach, and the function `random` is very helpful.

Here's the previous demo but with interactivity and randomness. The circle moves towards the mouse position, and shifts away from circle as time moves on. The code follows.

{{<240108-Genuary8-p5js-basics>}}

```javascript
//based on sketch from Generative Design
var formResolution = 10;
var radius = 50;
var angle;
var centerX;
var centerY;
var x =[];
var y =[];

var stepSize =1;

function setup() {
  createCanvas(windowWidth, windowHeight);
  
  angle = radians(360 / formResolution);
  centerX = width / 2;
  centerY = height / 2;

  // init shape
  for (var i = 0; i < formResolution; i++) {
    x.push(cos(angle * i) * radius);
    y.push(sin(angle * i) * radius);
  }

  noFill();
  stroke(0, 50);
  strokeWeight(0.75);
  background(255);
  
  frameRate(10);
}

function draw(){
  centerX += (mouseX - centerX) * 0.01;
  centerY += (mouseY - centerY) * 0.01;

  // calculate new points
  for (var i = 0; i < formResolution; i++) {
    x[i] += random(-stepSize, stepSize);
    y[i] += random(-stepSize, stepSize);
    // uncomment the following line to show position of the agents
    // ellipse(x[i] + centerX, y[i] + centerY, 5, 5);
  }
  
  beginShape();

  // first controlpoint
  curveVertex(x[formResolution - 1] + centerX, y[formResolution - 1] + centerY);

  // only these points are drawn
  for (var i = 0; i < formResolution; i++) {
    curveVertex(x[i] + centerX, y[i] + centerY);
  }
  curveVertex(x[0] + centerX, y[0] + centerY);

  // end controlpoint
  curveVertex(x[1] + centerX, y[1] + centerY);
  endShape();
}
```

### learning advice
I think looking at examples have been tremendously helpful (the genuary hashtag on twitter has a lot of awesome submissions!). And also producing. Even though right now I'm mostly borrowing concepts I've seen and combining them, I've learned a lot by just manipulating existing code. I have a tendency to be self-critical, so I'm constantly reminding myself that I need to be terrible to be bad to be okay to be good. So for now I'm going to produce a lot of not-so-great work, but eventually they will be not-so-bad. Check out my [twitter](https://twitter.com/desai_wang) for my genuary submissions!
