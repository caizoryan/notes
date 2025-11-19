# what is priority

Thesis: Understanding design vocabulary by reconstructing it in software.
#### introduce yourself
Hey everyone, I'm Aaryan. I'm a graphic design student. And I aslo code.
#### Explain stuff
Today I'm going to present a publication design tool that I've been working on and just break the tool down into the parts that make it whole and also talk a little bit about my process.

Say: The tool isn't a concrete thing or a single application but more like several seperate mutations of the same codebase that I've used for different tasks. 

But the thing that binds them all together is a shared vocabulary.

Describe typographic (?)
A typographic vocabulary encoded as code.

#### show the stuff
-> So before I dive into the process and the parts of the tool, let me give you a quick demo. 
> shows: demos + the outcomes

Describe typographic (?)
Earlier I mentioned that what binds these tool(s) together is a shared vocabulary. And this vocabulary is a typographic vocabulary that you get exposed to as a graphic designer. And I've been using programming as a tool to probe and understand this design vocabulary by reconstructing it in software.
So when I say vocabulary,
I mean the concepts of design -> point
But I also mean the named functions and mechanisms <- point

So my first intention was to make an alternative to Adobe InDesign. which is Adobe's publicaition software.

But because I was building this thing from scratch I was thinking of words such as recto, verso, grids, page numbers, folios, text boxes, and all of the bits and pieces that constitute this thing called a book. I started thinking more about this project in terms of parts of a book that make it a whole and how they relate to one another.

I'll explain what these words mean in a minute. Because I'm going to break these terms down when I get to the parts that make the tool, and its going to sound a little bit like How to make books 101...

So breaking down these vocabularies and thinking how can they be constituted in a software context.

#### the parts
So I start by thinking whats the first thing I need to do?

###### text
Draw text on a screen.

```
text("this is some text", 10, 20)
```

So I did that, and it worked. But then I realised, all of these values are in pixels. But I'm a graphic designer so I want points, picas, ems and inches.

###### units
So I write this some functions that will convert values from any one unit to pixels. 
```
 em = (v) => inch(v) / 6
 pica = (v) => em(v)
 point = (v) => pica(v) / 12
 inch = (v) => value * dpi 
 ... etc
```

so these take in values and calculate the pixel value equivalent. These units are just ratios of each other. 
But as long as these units work, everything will be in correct ratios. And I can work at a lower pixel density for performance but for exporting increase that and everything stays in the correct ratio.

Now that I have units and I can use these units instead of pixel values which would correspond to their physical positions on a printed page.
```
text("some other text", inch(1), inch(.5))
```

So the same way I can also create a letter size page
```
createCanvas(inch(11), inch(8.5))
```

Units somehow give this p5 canvas the validity of a letter size sheet. Like because I can say that this canvas is 11inches wide and 8.5 inches tall I can clock it that this is a letter size sheet. So I'm like ok, so what I need to do is just make the interaction with the p5 canvas be mediated through this vocabulary and I'll be making books!

###### spreads, recto verso & grid
When we're looking at books.

[show a picture of an open book]

We're not really looking at a single sheet of paper. We're looking at two folded pages, that come together to make a surface.

[highlight two pages to show a spread]

And this spread has a left side and a right side. In graphic design jargon the left page is called a verso and the right page is called a recto.

So just like we used units to validate the canvas as a sheet of paper, if we can somehow constitute this canvas as two pages, so the verso and recto, then we can think of this canvas as a spread.

So when I think of this structure, the first word that comes to my mind is Grid!
Grid's come in lots of configuration.
For simplicity's sake lets say 
- grid is split into two sides, recto and verso. 
Each side has margins, columns and and hanglines.
- You can use columns for horizontal positions and 
- hanglines for vertical positions

So the grid is a structure that helps us locate points on a page.

```
grid = ({
	width, 
	height,
	columnCount,
	hanglineCount,
	margins,
}) => {
  // recto -> width / 2 + margins... etc
  recto     = /* calculates x position */, 
  verso     = /* calculates x position */,
  columns   = /* calculates x positions */,
  hanglines = /* calculates y positions */,
}
```

This grid gives me a structure so that I can find positions for either of the pages, and divide them into columns and hanglines. 

[diagram of hanglines and columns]

```
let grid = Grid({width: inch(10), height: inch(8), ...others })
text("some other text", grid.recto + inch(1), inch(.5))

//or

text("some other text", grid.rectoColumn(2), inch(.5))
```

Essentially the grid along with the units make this p5 canvas legible as a spread of a book.

###### sequencing
Up until now we've been drawing single spreads. But books have multiple spreads.

So I need a way to represent a spread as code so it can be collected in a book. In that case, a spread is just a collection of drawable elements (text, shapes, images).

```
let spread = [
  ['text', 
	['text', "there's a circle on the spread!"],
	['x', ['rectoColumn', 2]],
	['y', ['inch', 1]]
  ],

  ['circle', 
	['radius', ['inch', .5]]
	['x', ['rectoColumn', 2]],
	['y', ['inch', 1]]
  ],
]
```
 I won't explain right now why they're arrays and not objects or bound functions here in the interest of time and coherency, but if you're interested please ask me later about it.

So then if we have these contents as data, we just need a function to draw these contents to a surface.
```
drawSpread = contents => {
  // clears screen
  // loops over content and draws each of them
}
```

And then implementing a book is easy. 
The function takes in an array of spreads a page number and then draw the spread at the given page number.
```
drawBook = spreads, pageNumber => {
  drawSpread(spreads[pageNumber])
}
```

Ok so we make a bunch of spreads, pass it to draw book, see all these spreads, edit if we need and that's it we can print it out and we're good right?
right?

###### imposition
But there's one critical problem. If we look a book, what we percieve as spreads are separate sheets. A spread gets viewed as one surface but is printed on separate sheets (except the one in the middle of the signature).

So the spreads have to be drawn virtually, split into individual pages and imposed onto several different sheets in a way that then can be bound together to form a booklet. 

So if you're doing 2 sheets of paper, that gives you 4 spreads (surfaces). 
[show sheets]
[show a flip through]

which means the configurations needs to be something like:
[show configuration of sheets]

This is the algorithm for it
[sketchbook image]

This is also the algorithm 
[video of shuffle]

This is how I figure out difficult problems sometimes. I just record myself or draw and try to identify the patterns.

Anyways, I finally figured it out and the current implementation looks something like this.

[image of the code]

I won't explain this because I'll run out of time.

and finally I just need so I can make pairs of any 2 pages based on the configuration I need for printing.

```
versoImage = spread => {
  // draw spread to a buffer
  // clip out the verso region using grid
  // return image
}

rectoImage = spread => {/*same stuff*/}

drawPair = 
  (spreads, [rectoPage, versoPage]) =>
{
  // get the recto and verso images using spreads
  let recto = rectoImage(spreads[rectoPage])
  let verso = versoImage(spreads[versoPage])

  // draw them on current canvas
  img(verso, 0, 0)
  img(recto, grid.recto, 0)
}

```

So with this now I can design spreads
[show spreads]

export as shuffled
[show saddle view]

print them out and bind them as a book.
[show printed]

So with all of this in some sense I have a complete publication tool!

#####  After imposition.
So upon figuring this out, I found 3 critical things that changed my perspective on what this tool or this project was.

1. Spreads are virtual surfaces. which means they can be designed as a surface separate from the actual physical surfaces
[show an example of virtual surface across two bookelts]
[show a booklet cut fold]

2. Making a publication software is just about reconcilling physical sheets and virtual surfaces (spreads)
(+ also represent a view of the final form)
[show using different color sheets] -> reconciling sheets
[show vertical offset] -> representing a view of final form
[so page numbers aren't discrete but continuous]

3. I can play with the syntax and mechanics of what words mean when the vocabulary is constructured. And use this as an affordance to alter the form of the book.

