# EAD 

### Reflections
Just finished the EAD project with craig. First collaborative project with this tool using the discussion method[^1].  Learned a lot of things from the fact that--

1. We were working with long text (and linked textboxes weren't working)
2. Large set of pages and content + moving things around often
3. Using mainly the UI for editing and content movement... 
4. Having someone to work with who could give me feedback on type in terms of the (programming) language I was working with.

Working on a type not as a means to test out things I implemented but rather in service of the type. So desigining it as I would any composition and then desiring a certain graphic technique to alter the composition (baseline shift, linebreak on word patterns, etc). Then implementing these things. 

This shift in perspective oriented me towards a certain task rather than loosely going along implementing stuff. 

I think the recursive way of implementing documenting that I've been doing hasn't worked out for me. Because it launches me onto tangents rather than consolidating effort towards more practical things. So I'm going to orient the making towards specific projects, take a week to implement what reflections come out of the project and repeat.
	
### Things to improve
...in the tool

##### Production
One of the pain points during production was incorrect sizing. This was happening because we were printing the pages as jpegs. I need to figure out a way so that the file that is printed is set to be the size of the sheet. So maybe a solution can be creating a pdf that has the image set on the fullsize page including the cropmarks and bleeds. 

- Take exported images and place them on a pdf page.
- Also implement bleeds

The other thing I was also considering is seeing how feasible a direct pdf backend would be to implement. I think if I'm working mainly with text, image and svgs it shouldn't be that hard.

This -> [pdf-lib](https://github.com/Hopding/pdf-lib/blob/b8a44bd24b74f4f32456e9809dc4d2d9dc9bf176/src/api/operations.ts) seems like a good option to try out for that.

- Expriment with pdf-lib and try print some stuff using it. Also see if you get access to CMYK layers or something, or maybe you can tweak overall file colors or something...

	
##### User Interface

###### Loading and saving files
> I need to find a good way to load and save files and have version histories.

One constant problem was the ability to load and save files. The current datastructure is just saved to to local storage so it persists if you work on a single project. But switching projects is hard. I was saving the files by just downloading it. But maybe I should implement a simple server to store and swap working files.

###### Views for certain components
> Implementing views for text frame and paragraph styles and stuff, so textframes can be visually distinguished as text frames.

After a point when there is a lot of content on the screen, browsing the datastructure trees gets extremely cumbersome. The general solution is using mouse to drag elements directly on the canvas. I'm wondering if rather I will be able to just fine tune the typography of the ui so browsing the datastructure trees can be a little more intuitive. 

In general I want to maintain the distance the designer maintains from the elements on the canvas, so elements can be seen as the result of properties and mechanics set in the datastructure rather than absolutely placed by dragging them.

###### A fold all and unfold all function- 
> For easier browsing...

###### Filters
Filters, show only arrays with certain fn symbols... So show me only textFrames or show me only Loops etc. Have it so if there is a nested textframe inside a loop, even that should show etc.

###### Return of the grid
> reimplementing a grid
And then having a ui for the grid. Implement the grid just as an object, and the values in it can just be value acceses[^3]. Maybe there should also be UIs for symbols. [^2]

Grid can produce x and y locations, or maybe x y and rotations? if I want on a slanted line or smth... Maybe hooks to put words on the page? so it can go in a type of rythm?
	
###### Panning & zooming
Make ui for zooming into the canvas... and moving it around. Take a look at glyphs drawing app. or smth its called.

###### Multiselection
This could be a tricky one but if implemented would be super cool. It can be implemented by changing the cursor to anchor and head.
Also think about how the idea of lines and letters can be implemented with the tree structure(?)

###### Sheet editor
- Maybe a sheet datatype view
so color, width/height can be used to produce a view of different type of sheets which will make using them easier.

###### Toggle live mode
So you can edit things and not get errors constantly.
	
##### Technical stuff
Rewrite the scale. Right now units are formatted so they store what units they are. But I don't ever use the units post execution. Units in the UI are always only represented as pre-execution:

```
['em', 1]
['inch', 1]
```

Etc. So might as well have them as simple functions that just return a number instead of packing the number in a .px

I think doing the talk for creative coding, and trying to make it as simple as possible for reception actually made me realise... well it could just beeee that simple. 

So same thing for grid as well.

Also wondering if there can be a way to implement a simple undo redo. Have to see how to do transaction based editing of arrays so they're reversible and trackable.

	
# Footnotes
[^1]: Sort of like pair programming. A way of working where collaborator is the hands, does the actual execution of software so to produce the print file, and the other helps in making decision and discuss design elements.

[^2]: Another thought... the ```key``` function could be a drop down view. But I would need to 

[^3]: I think doing the talk for creative coding, and trying to make it as simple as possible for reception actually made me realise... well it could just beeee that simple. 
