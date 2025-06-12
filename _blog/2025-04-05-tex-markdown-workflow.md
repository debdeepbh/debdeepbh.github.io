---
title: Writing with markdown and TeX
tags: tex markdown pandoc mathjax marp
---

{% include math.html %}



$$
\newcommand{\xx}{\mathbf{x}}
\newcommand{\R}{\mathbb{R}}
\newcommand{\ww}{\boldsymbol{\omega}}
$$


$$\begin{CD}
A @<<< B @>>> C\\
@. @| @AAA\\
@. D @= E
\end{CD}$$

New command $$\xx$$ and $$\R$$ and $\R$ and $\xx$ and so on and so forth and $\ww$ and $\lesssim$ $\textcolor{blue}{Hello}$ and $\boldsymbol{\omega}$

Inline math:  $$x^2$$ vs $x^2$

vs

$$
\begin{align*}
x^2
\end{align*}
$$

vs

\begin{align}
x^2
\end{align}

# Tex and markdown conversion to html with pandoc

- To use latex goodies such as snippet completion etc in vim, set 

```vim
:setfiletype pandoc.tex
```


- Put all latex preamble in the header part of the `.md` file [source](https://pandoc.org/MANUAL.html#extension-yaml_metadata_block) like this

```yaml
---
title: Readme
author: Author
header-includes: |
    \usepackage{amsmath, amssymb, amsthm, amsfonts, color, bm}

    \newcommand{\R}{\mathcal{R}}
    \newcommand{\ww}{\boldsymbol{\omega}}
    \newcommand{\xx}{\mathbf{x}}
---
```

Converting a tex file into html `pandoc file.tex -o file.html` uses unicode by default to render math symbols. We need to use `mathjax` for a nicer rendering. Other options are

```
--mathml, --webtex, --mathjax, --katex
```

and demos can be found in pandoc [demos](https://pandoc.org/demos.html).

According to [pandoc documentation](https://pandoc.org/chunkedhtml-demo/3.6-math-rendering-in-html.html) One need to specify the url of the `.js` file that would be used to convert math into mathjax. By default pandoc uses some link form some content delivery network (CDN), which does not work on firefox at the first attempt. So we can specify the url like this:

```bash
pandoc math.text -s --mathjax=https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js -o   mathMathJax.html
```

There are other CDN locations on [mathjax documentation](https://docs.mathjax.org/en/latest/web/start.html#cdn-list) from sites like

- jsdelivr.com [latest or specific version] (recommended)
- unpkg.com [latest or specific version]
- cdnjs.com
- raw.githack.com
- gitcdn.xyz
- cdn.statically.io

```bash
pandoc README.md -s --mathjax=https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js -o   README.html
```

## LaTeX writing guide

We want our `.md` file to convert to pdf or tex without much hassle. While using mathjax, a few things to remember for a quick conversion.

- Tex environments should **not** be within `$$`s. For example, 

    ```pandoc
    $$
    \begin{align*}
    x^2
    \end{align*}
    $$
    ```

    is not desired. The correct version (desired by pandoc+mathjax) is:

    ```
    \begin{align*}
    x^2
    \end{align*}
    ```


    This causes some pain since `vim-pandoc` does not render the math symbols within the environments in vim. Surprisingly, converting a tex file to md puts `$$`s around latex environments. So weird.


- If you are using `\usepackage{bm}` for bold fonts and using commands like `\boldsymbol{\sigma}` etc (apparently better alternative to `\pmb{}`), make sure to put braces around it when using as subscript or superscript. For example, use `f_{\boldsymbol{\sigma}}(x)` instead of `f_\boldsymbol{\sigma}(x)`. The second usage will put `(x)` also within the subscript when you convert it into tex. This is a very weird behavior since you would think both are Tex commands.


- Bullet points: make sure to leave an empty line before the first top level bullet point. For sub-bullet points, no need to have empty line. Empty lines between bullet points makes the bullets more sparse.

## Diagrams

My observation is that using a freehand drawing tool like inkscape takes less time and provides more flexibility for creating diagrams. Markdown-friendly tools like `mermaid` required additional set up and does not seem to support latex within diagram. Maybe once can use latex `tikz` diagrams within markdown, but the whole point was to move away from programmable diagrams. Still:

Install pandoc filter for mermaid from [git](https://github.com/raghur/mermaid-filter?tab=readme-ov-file) using

```
npm install --global mermaid-filter
```

Use it with `-F` in pandoc

```
pandoc  -F mermaid-filter something.md -o something.html 
```

A sample block of code 

```pandoc
```{.mermaid format=png scale=5 caption='Computational graph'}
%%{init: {'theme':'neutral'}}%%
  graph TD
    a --> b
```
```

produces a flowchart-like diagram.

## Marp and usual markdown

Converting marp-focused `.md` file into html using `pandoc` is very glitchy. Few things that do not work so far

- Putting latex preambles to the yaml header
- Custom css for creating columns: math within the custom css does not render. Pandoc is not able to accept the marp theme css
- Bullet points render in a single line
- 

## Github readme compatibility

The markdown files with header does not render in github webpages, even though both are mathjax.
