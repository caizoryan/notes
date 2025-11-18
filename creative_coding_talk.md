## Chunks

####   Introduce.
hi, my name's Aaryan.

I'm a graphic designer (student). 
I also code. 

Today I'm going to present a publication tool I've been working on for the past few months.

######  ---
I started on this path because I was seeking an alternative to Adobe in general. So I thought to myself what would it take to bootleg something like InDesign

I dont want to focus on what this tool can do, but rather on the process of how this thing came to be, and how language and syntax influences this process.

But I'm still going to show you the tool cause I think its super cool!

###### first box 
So, here's the tool.
Essentially is a p5 canvas, with typographic vocabulary.  The datastructure is nested arrays.

- you can put words on a "page"
- you can put more words on a "page"
- you can put images
- and shapes
- and more shapes

- Change sheet sizes
- And colors
- You can offset pages vertically
- You can offset pages horizontally
- See how this would look at each page intersection
- For different books
- And multiples

- And export as imposed print files
- Which can then be bound

###### xxx. 
So now that you've seen the tool
Lets break this down to the bits and pieces. 

###### xxx. 
We have terms like page, spread, grid, signatures, sheets, points, picas,  and all of these bits and pieces of natural language constitute this thing called a book. 
[a transition of all the listed words and them as classes]
I've been using programming as a tool to investigate what these words mean and how they relate to one another.

<!-- Most of this tool is just giving meaning to this vocabulory in a computer graphics context. And using that vocabulory to make surfaces legible as elements of a book. And I'll explain what this means... -->

###### Typesetting
The first thing that comes to mind when you think of a software that can make books, is: words.

place text box at x and y position
(use pixels)

etc...

###### Units
Ok so whats next? I have words on a white box, but how can I turn this white box into paper?

I can print it... but it won't look the same. And also a bit blurry (which might have to do with the DPI/PPI)

So I probably need a scale and units so the canvas can correspond to the printed page, and maintain it for different DPI's 

So here's the units you'll probably see in CSS, this is the stuff we use in our day to day when talking about type.

real units -> [em, inch, point, pica]

re-show text box but use units instead of pixels

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
So up until now we've been working with a single spread. But books have multiple spreads.

so this is easy, create a book class, have it store spreads and a current spread variable. And just draw the current spread.

Book stores spreads, book.draw() draws current spread

###### Imposition 
So here's the fun part. If you take a close look at a book, you'll see that the spreads aren't really on the same sheet. They get split up into different sheets so the can be bound at the center. 

imposition
[explain imposition]
[single signature, two signatures]
	
###### Steering 
till now I was bootlegging indesign which I had valid reasons for...
I needed software alternatives to Adobe

but that didn't seem enough, because there already exist these alternatives. What was I gaining from building something like this from scratch?

I needed to utilize the affordances that came from building this tool from the ground up.

And I had just spent all this time trying to figure out imposition. So naturally I started messing around with this.

###### Vertical offsets
vertical offsets -> where do pages/spreads get rendered

###### Horizontal offsets
horizontal offsets -> this one is a little bit more tricky...
because with verical offsets I could just draw pages at an offset,
but with horizontal offset, 
[page sizes change]
So cant rely on page size to be same, so page sizes have to be derived from sheets, checking  

###### Accordion books
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
