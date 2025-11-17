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

###### ---
The first thing that comes to mind when you think of a software that can make books, is: words.

So, lets start there. To display a word--
You need the word, x and y position.
To display multiple words, you need the start position, line length and height. Loop over the words and when the words length exceeds line length increment y position and start again.

[basic algorithm, x, y, word length, line length]

I know p5 can do this for you, but if you write this from scratch you can hook into the process and do cool stuff like this:

[show type hooks]
(map word length to weight)

etc...

###### ---
Ok so whats next? I have words on a white box, but how can I turn this white box into paper?

I can print it... but it won't look the same. And also a bit blurry (which might have to do with the DPI/PPI)

So I probably need a scale and units so the canvas can correspond to the printed page, and maintain it for different DPI's 

So here's the units you'll probably see in CSS, this is the stuff we use in our day to day when talking about type.

real units -> [em, inch, point, pica]

###### ---
So now 
[em, inch, points] -> become units now to find and place stuff on surface
grid to make legible space

###### --- 
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

vertical offsets -> where do pages/spreads get rendered


###### ---
horizontal offsets -> this one is a little bit more tricky...
because with verical offsets I could just draw pages at an offset,
but with horizontal offset, 
[page sizes change]
So cant rely on page size to be same...


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
