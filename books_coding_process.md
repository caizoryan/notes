# Wowa-weee

### Classes, Functions, Process

Talk about the process of going from class based programming to a functional sense

Talk about going from generic book structure (link it to classes) to segmenting out book parts and how this helped in iterating on structures

I started off just wanting to make a publication software. So what do you need to make that.

- draw spreads
- output those spreads imposed on a sheet so they can be bound

What do you need to 

##### Draw spreads
To draw spreads, you need content to draw on it. To start off I'm thinking just text. Textboxes, Linked textboxes and maybe images.

**Edge case**: Think about whats the most meaningful way of drawing cover and backcover
> Answer : Treat them as spreads where on the front cover, the verso is not drawn and on the backcover the recto is not drawn. This way they can still be treated as spreads.
	
##### Draw paragraphs
So what do you need to draw paragraphs?

- typesetting algroithms 
  - alignment
  - lineheight
  - fontface

Describe this briefly

##### Imposition
How do you export and print?
> Have to reconcile spreads and sheets
So you need to be able to separate verso and recto so you can split them on the 'actual' sheets. This can then be bound.

So once I had all of this down, I was like niceee! now what is indesign not letting me do? I'm going to start experimenting with all of that.

I started off with just playing around with text. So having hook functions before each stage of the rendering. So I can calculate color based on position or font-weight based on word length, etc.

Then I started thinking, Ok it was really fun to figure out the whole imposition shennanigans, I wonder if I can play around somewhere there.

I had done this book before: (RM 1) 

So I thought, ok perhaps I could make a view in this tool that will render something like that.

To do an offset like this, I would need to see which page belonged to which spread. And then alter its position when rendering based on the data in the sheet structure.

and then I had vertical offsets!

