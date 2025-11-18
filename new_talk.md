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
-> Before I talk about it, here are some demos:
> shows: demos + the outcomes

Describe typographic (?)
Earlier I mentioned that what binds these tool(s) together is a shared vocabulary. And this vocabulary is a typographic vocabulary that you get exposed to as a graphic designer. And I've been using programming as a tool to probe and understand this design vocabulary by reconstructing it in software.

// so my first intention was to make an alternative to indesign. If you don't know indesign its a software used to make books.

But because I was building this thing from scratch I was thinking of words such as recto, verso, grids, page numbers, folios, text boxes, and all of the bits and pieces that constitute this thing called a book. 

I'll explain what these words mean in a minute. Because I'm going to break these terms down, this is also going to sound a little bit like How to make books 101... but yeah.

Anywas, I'm at this starting point and I have no conceptions of how these terms will translate from words into a working thing. So I was building all of this from scratch,

I think to myself, ok I have the syntax that is afforded to me by javascript and p5 and they can make things appear, and I have to use this to somehow encode typographic concepts. From scratch.

So breaking down these vocabularies and thinking how can they be constituted in a software context.

So I start by thinking whats the first thing I need to do?

Draw text on a screen.

```
text("this is some text", 10, 20)
```

So I did that, and it worked. But then I realised, all of these values are in pixels. But I'm a graphic designer so I want points, picas, ems and inches.

So I write this some functions that will convert values from any one unit to pixels. 
```
 em = (v) => inch(v) / 6
 pica = (v) => em(v)
 point = (v) => pica(v) / 12
 inch = (v) => value * dpi 
 ... etc
```

Now that I have units and I can use these units instead of pixel values which would correspond to their physical positions on a printed page.
```
text("some other text", inch(1), inch(.5))
```

So the same way I can also create a letter size page
```
createCanvas(inch(11), inch(8.5))
```

But when we're looking at books.

[show a picture of an open book]

We're not really looking at a single sheet of paper. We're looking at two folded pages, that come together to make a surface.

[highlight two pages to show a spread]

And this spread has a left side and a right side. In graphic design jargon the left page is called a verso and the right page is called a recto.

So I somehow need to be able to access the right page, the recto.

So I would need an object that knows the spread size (different from page size). So this object can divide the width by 2 to get the position of where the right page would start.

And where better to store this than the grid. The grid as a structure that helps locate points on a page.

```
grid = spread dimensions => {
  recto = position,
  verso = position,
  columns = position,
  hanglines = position,
}
```

This grid gives me a structure so that I can find positions for either of the pages, divide them into columns and store hanglines. 

[diagram of hanglines and columns]

Essentially the grid along with the units make this p5 canvas legible as a spread of a book.

```
let grid = Grid({width: inch(10), height:inch(8)})
text("some other text", grid.recto + inch(1), inch(.5))

//or

text("some other text", grid.rectoColumn(2), inch(.5))
```

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
	['x', ['rectoColumn', 2]],
	['y', ['inch', 1]]
	['radius', ['inch', .5]]
  ],
]
```
And a function to draw these contents to a surface

```
drawSpread = contents => {
  // clears screen
  // loops over content and draws each of them
}
```

And then implementing a book is easy. 
The function takes in spreads -> list of spreads and a page number and then draw the spread at the given page number.
```
drawBook = spreads, pageNumber => {
	drawSpread(spreads[pageNumber])
}
```

Done! we can print this out and we're good :)
right?

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

// After imposition.
So upon figuring this out, I had found 3 critical things that (sometting tsomething)

1. Spreads are virtual surfaces. which means they can be designed as a surface separate from the actual physical surfaces

2. Making a publication software was about reconcilling physical sheets and virtual surfaces (+ represent how the post production view of this reconcillment would look like)

3. I can use the above 2 things to make so many different types of books!


Once I figured out this distinction
