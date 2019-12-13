---
layout: post
---

## Reveal.js for linguistics: using Markdown to write slideshows

## What is Markdown

Markdown is a markdown language that uses an extremely simple syntax, which then gets formatted correctly in the output. 
The writer writes the files in plain text, and uses special tags for simple formatting.
For instance enclosing text in asterisks will render as italics in the output: `*in the source code, this block is enclosed with italics*` will yield *in the source code, this block is enclosed with italics*.
Enclosing text in `**double asterisks**` will output as **boldface**
Similarly, writing the following:

```
- Some sentence here.
- Another here.
- And another here.
```

will yield a bulleted list:

- Some sentence here.
- Another here.
- And another here.

Markdown is increasingly being used in many many ways, as it has the advantage of being very simple to write, having a lot of support in applications that are based in plain text, as well as the added bonus that the source files are very easy to read.
Markdown compares very favourably in this regard to, for isstance, text that is written for LaTeX processing.

Here is not the place to discuss markdown in any comprehensive way, but there are good discussions online (LINKS).
Important for here is that it makes it very easy to write slide shows, handling most of the general formatting you need for your slides.
Although reveal.js is a framework that at its most basic uses .html input, it works very well with reveal.js, making it very easy to quickly create slide shows.
**Note**: there are clear limits to markdown, which I'll discuss later on.

There are in fact two ways in which one can write the source file in Markdown for use with a reveal slide deck, and I will discuss each in turn here.
Each has benefits and drawbacks, which I'll try to highlight.

## Using Markdown for Reveal.js: Method 1

Positives

## Using pandoc

It is also possible to use [pandoc](Https://pandoc.org),  which is freely available, cross-platform document conversion software.
If.you are downloaded from a package manager, ensure that you update to the most recent version, which is XX. 

Pandoc is a command line utility that is able to convert text files between a number of formats and into a variety of outputs. 
For our purposes, it is able to convert a markdown file into a hmtl file with all the necessary reveal.js boilerplate.
**Important**: you still need to download or clone the reveal.js repository and place the pandoc output in the right place.

### Basic use

To create a simple slide deck, write the content in markdown.
Then, in a terminal window run the following, substituting the capital letters for your relevant file names:

```
pandoc -t revealjs INPUTFILE.md -s -o OUTPUTFILE.html
```

If you want bullet points to be uncovered one by one, then include the option -i

```
pandoc -t revealjs INPUTFILE.md -s -i -o OUTPUTFILE.html
```

The output of this command will be a file with all the necessary reveal.js boilerplate, and your markdown file converted into HTML.
The file should then be placed in a position where the links to the relevant reveal.js files can be located.
By default, this is the directory **above** the reveal.js you cloned earlier.
So, it should look as follows:

[IMAGE OF FILE PATH](img)

## Customisations

Whilst the above will create a fully functioning reveal.js slide deck, you may wish to customise it further.
For instance, the default theme is the 'black' theme, but can be changed in the following way:

```
-V theme=$THEMENAME
```

Any of the variables that can be set in the configuration of reveal.js can be tweaked this way. 
For instance, if you wish to change the transition speed and use the beige theme, you can use:

```
pandoc -t revealjs INPUTFILE.md -s -i -o OUTPUTFILE.html -V theme=beige -V transitionSpeed=fast
```

Citations can be added using regular markdown citation syntax, and running with the `filter  pandoc-citeproc` option.
Note that you should then specify the path to the bibliography in the metadata of your markdown file.
For instance:

```
---
title: Hello
author: Peter
date: today
bibliography: /path/to/your/bibliography
---
...
```

```
pandoc -t revealjs --filter pandoc-citeproc INPUTFILE.md -s -o OUTPUTFILE.html
```

Finally, trees can be added in as an image file.
There may be ways to first run them through latex to output them as an image file automatically (see a discussion from Pavel Iosad [here](https://www.anghyflawn.net/blog/2014/teaching-slides-with-pandoc-and-reveal-js/), so it is possible to do it like this.


To cover:
- installation of pandoc (ensure current version)
- basic use
- file structure
- adding options on command line
- custom templates (and other customisations)
- citations
- trees

Downsides:
- no live update
- some Javascript issues