## Chunks

####   Introduce.
hi, my name's Aaryan.

I'm a graphic designer (student). 
I also code. 

Today I'm going to present a publication tool I've been working on for the past few months.

######  ---
I started on this path because I was seeking an alternative to Adobe in general. So I thought to myself what would it take to bootleg something like InDesign

I dont want to focus on what this tool can do, but rather on the process and how language and syntax (natural and programming) influences this process

But I'm still going to show you the tool cause I think its super cool!

###### first box 
So, here's the tool.
Essentially is a p5 canvas, with typographic vocabulary that live in the datastructure.  The datastructure is nested arrays (which I've been trying to turn into a DSL but that isn't fully resolved so I won't be talking about that).

Anyways, so...
- you can put words on a "page"
- you can put more words on a "page"
- you can put images
- and shapes
- and more shapes

- You can offset pages vertically
- You can offset pages horizontally
- Change sheet sizes
- And colors
- See how this would look at each page intersection
- For different books
- And multiples

- And export as imposed print files
- Which can then be bound

###### xxx. 
So now that you've seen the tool
Lets break this down to the bits and pieces

###### xxx. 
As designers we spend a lot of time making and engaging with books

So I'm interested in terms like page, spread, grid, signatures, sheets, points, picas,  and all of the bits and pieces of natural language that constitute this thing called a book. 

When I start to **program** and think of **ways in which books can be taken apart or reconstituted**, I have to depart from a natural language to something else (a fuzzy space) where like natural language becomes coded or syntax.

[a transition of all the listed words and them as classes]

I've been using programming as a tool to investigate what these words mean and how they relate to one another.

###### Typesetting
The first thing that comes to mind when you think of a software that can make books, is: words.

So, lets start there. To display a word--
You need the word, x and y position.
To display multiple words, you need the start position, line length and height. Loop over the words and when the words length exceeds line length increment y position and start again.

[basic algorithm, x, y, word length, line length]

I know p5 can do this for you, but if you write this from scratch you can hook into the process and do cool stuff like this:

[show type hooks]
(map word length to weight)

etc...

###### units
Ok so whats next? I have words on a white box, but how can I turn this white box into paper?

I can print it... but it won't look the same. And also a bit blurry (which might have to do with the DPI/PPI)

So I probably need a scale and units so the canvas can correspond to the printed page, and maintain it for different DPI's 

So here's the units you'll probably see in CSS, this is the stuff we use in our day to day when talking about type.

real units -> [em, inch, point, pica]

###### grid (recto verso)
So now we can use these units to place things on the surface.
But if I wanna say place this text box on the right page. It becomes cumbersome because I have to get the width, / by 2 and the get the start position for right page etc, etc.

So I need to make this surface legible as a spread. 
-> whats a spread
a spread is when you see an open surface in a book, so both the right and left page combining to form a surface. The term for these pages (left and right) is (verso and recto)

right -> recto
That's how I remember it.

-> has a recto and verso

How do we make it legible -> grids!
Grids store the spread size, calculates the center, and generally makes the surface legible as a spread. 

Just like the units turned the canvas context into a page, grid turns the page into a spread. (also the fact that the page is folded helps)

I also like thinking of the typographic grid as making the surface legible just as a programs make legible memory on a computer.

###### Sequencing spreads
So up until
Book stores spreads, book.draw() draws current spread


###### --- 
So here's the fun part.
imposition
[explain imposition]
[single signature, two signatures]

###### --- 
till now I was bootlegging indesign which I had valid reasons for...
I needed software alternatives to Adobe

but that didn't seem enough, because there already exist these alternatives. What was I 
gaining from building something like this from scratch?

I needed to utilize the affordances that came from building this tool from the ground up.

And I had just spent all this time trying to figure out imposition. So naturally I started messing around with this.

###### V ertical offsets
vertical offsets -> where do pages/spreads get rendered


###### Horizontal offsets
horizontal offsets -> this one is a little bit more tricky...
because with verical offsets I could just draw pages at an offset,
but with horizontal offset, 
[page sizes change]
So cant rely on page size to be same...

######  Accordion books
Renaming Book to Signature

###### Virtual Spreads
All spreads are virtual. 

###### --- 
So once more
you can put words on a "page"
you can put images
and shapes

You can offset pages vertically
You can offset pages horizontally
Change sheet sizes
And colors
See how this would look at each page intersection
See this for multiple signatures
See this for different book forms

And export as imposed print files
Which can then be bound

######  ---
I've been using programming to investigate what these words mean and how they relate to one another

######  ---
So i'm going to spend majority of the time talking about how the tool came together
and how its working parts relate to each other


## Transitions
1. px, to other units
2. using grid to locate & page size
3. recto verso spread
4. sheets (imposition)
5. vertical offset sheet
6. (page size stored in sheets) horizontal offset sheet
7. oh! offsets are sheets
8. book -> signature
9. functional (...not really) (decoupling state)

---
10. page numbers
11. alt impositions
