# Reveal.js for linguistics: Creating a talk with reveal.js


## What is reveal.js

There are many options to create slide decks, each with their own benefits and drawbacks.
By far the most popular, and the ones overwhelmingly seen during talks, are dedicated slideshow software such as [Microsoft Powerpoint](LINK) or [Keynote](LINK) from Apple, or slides created through LaTeX using beamer.
Other options such as [prezi](LINK) will also output slides.

[Reveal.js](link) is a javascript library that creates a slide deck by writing in html.
That means that the source code is plain text, and all it needs is a browser to run.
Therefore, they are independent from a particular operating system (unlike powerpoint and keynote).[^1]

[1: Yes, I know that you can run powerpoint on Apple, but it never works *quite* as well as you'd hope.]

## So, it's beamer?

The two have in common that the source files are both written in plain text, however the difference is that a beamer presentation will be run through LaTeX to create a pdf file, whereas a reveal.js presentation is rendered as a webpage.
The key difference between them is that beamer files are *static*, as pdf files, whereas reveal.js slides can be *intereactive*, as they are effectively a web page.
Any interactive web content can therefore be used.
The benefit here is that media can be directly played (videos, sound clips) and that diagrammes can be created that are interactive.

Another difference between the two is the flexibility with regards to appearance. 
Whilst beamer presentations can be styled according to pre-built (such as XYZ, or the *very* nice [metropolis theme](LINK)) or custom templates, reveal.js can be styled using javascript and css.
This gives more flexibility, since all that is required is relatively rudimentary css skills, and properties can be assigned 'on the fly' according to the needs of the user.
This is not to say that you can't do similar styling with beamer, it is just easier and quicker in my experience to do it with css.

## Drawbacks vs. beamer

Mostly, the process of making reveal.js slides works in much the same way as with beamer, with the only major difference being the markup language.

```
\begin{frame}
\begin{itemize}
\item Here is a bullet point.
\item \textit{With another written in italics}.
\item \textsc{And another in small caps}.
\end{itemize}
\end{frame}
```

Is broadly equivalent to (with italics and small caps defined in a css file):

```
<section>
<ul>
<li>Here is a bullet point</li>
<li><span class="italics">With another written in italics</span>.</li>
<li><span class="smallcaps">And another in small caps</span>.</li>
</ul>
</section>
```

In practice however, the markup language differences will have little to no effect on the writing process --- aside from a couple of specific instances, discussed below --- as a good text editor with snippet support will result in the same number of keystrokes being used to add in all of the surrounding markup, so the writer can focus on the content.

The areas where there are noticeable differences for specifically linguists come in three areas: citations, examples and tree drawing.
All of which are easily integrated into the LaTeX workflow through different packages , notably `biblatex/natbib` in the former case, `gb4e/linguex` for examples, and (some variant of) `qtree/forest` in the latter.
The big advantage of using these is that they directly integrate with latex and fit seamlessly into the text: these are compiled at the same time as the text., with the result that the native formatting of the paper and slides is used.
Furthermore, in the case of citations they can be formatted according to the usual standards of the field.

Those accustomed to writing papers and slides in LaTeX will find initially that these aspects of reveal.js are less intuitive for their workflow, however, there are ways around them, which are equally, or near equally good.

## Citations

The first instance is with citations. 
Ususally, at the end of a paper, one will find a list of citations like below:

![citation image](/assets/img/citations.png)

Usually, academics carry this over to slides as well, particularly if writing in beamer, given that the commands are the same.
Unless one uses pandoc to generate reveal.js slides --- see [here](LINK) for a how to, including advantages and disadvantages of this --- there is no direct way to generate a citation list as given in the example above. 
HTML and css do not support bibliography management as far as I know, and whilst one can export a citation list using Zotero or Refworks (CHECK THIS) into HTML and incorporate that into your slides, this is still indirect, and is vulnerable to forgetting to include citations.
One of the great things about LaTeX is that you need only include `\citet{reference}`, run biber/bibtex and it will appear there.

Since reveal.js does not offer this system then one has to change things a little.
The obvious change, and the one that I use is to simply adapt to the system one is using and link your citations as hyperlinks in the slides.
For instance:

```
<section>
<ul>
<li><a class='citation' href="moskalglossa">Moskal (2018)</a> has argued that suppletion is never seen for the inclusive alone.</li>
</ul>
</section>
```

The above will render as the following (with styling of the citation link done in css).
The benefit of doing it like this is that one allows the audience to see the citation, and if they are following the slides along on their own device (it's very easy to host slides online before your talk, for instance on github, or a personal website).
The downside is that the audience cannot check a reference list in realtime to see what 'Moskal (2018)' (in the above example) refers to.
However, I think that this is a relatively minor drawback, especially if one is already hosting the slides online.


## Trees

Again, the major benefit of using LaTeX is that there is a large amount of packages ready for use that have been developed over the years. 
Given that reveal.js is a relatively new framework for making slides, and that it is not often used by adcademics, such packages are missing.
This is starkly the case with tree drawing, something that is really easily handled by `qtree/forest` using LaTeX.


```
\begin{tikzpicture}[baseline]
\Tree [ [ A woman ] [ saw [ a dog ] ]
\end{tikzpicture}
```
