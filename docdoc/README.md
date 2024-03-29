<!-- SPDX-License-Identifier: CC-BY-SA-4.0 -->
<!-- SPDX-FileCopyrightText: 2020 The LumoSQL Authors -->
<!-- SPDX-ArtifactOfProjectName: LumoSQL -->
<!-- SPDX-FileType: Documentation -->
<!-- SPDX-FileComment: Original by Dan Shearer, 2020 -->

# Explaining the LumoSQL Documentation Project

This is documentation about documentation, covering how the LumoDoc project
goes about maintaining the documentation for the LumoSQL project.

The actual docs for LumoSQL database project are [here in the doc
directory](https://lumosql.org/src/lumodoc/file?name=doc/README.md). A very few
of the most detailed technical documents are stored in 
[the LumoSQL repository](https://lumosql.org/src/lumosql) with the source code they relate
to.

Table of Contents
=================

   * [LumoSQL Documentation Standards](#lumosql-documentation-standards)
   * [Contributions to LumoSQL Documentation are Welcome](#contributions-to-lumosql-documentation-are-welcome)
   * [LumoSQL Respects Documentation for SQLite, LMDB and More](#lumosql-respects-documentation-for-sqlite-lmdb-and-more)
   * [Text Standards and Tools](#text-standards-and-tools)
   * [Diagram Standards and Tools](#diagram-standards-and-tools)
      * [LumoSQL Diagram Signature](#lumosql-diagram-signature)
      * [Using the LumoSQL Diagram Library](#using-the-lumosql-diagram-library)
      * [Adding Diagrams](#adding-diagrams)
      * [Diagram Style Guide](#diagram-style-guide)
   * [Image Standards and Tools](#image-standards-and-tools)
   * [Previewing Markdown before Pushing](#previewing-markdown-before-pushing)
   * [Copyright for LumoSQL Documentation](#copyright-for-lumosql-documentation)
   * [Metadata Header for Text Files](#metadata-header-for-text-files)
   * [Human Languages - 人类语言](#human-languages---人类语言)
   * [Creating and Maintaining Table of Contents](#creating-and-maintaining-table-of-contents)
   * [Tidying Markdown (mostly not required)](#tidying-markdown-mostly-not-required)


LumoSQL Documentation Standards
===============================

This chapter covers how LumoSQL documentation is written and maintained. 

![](../doc/images/lumo-doc-standards-intro.jpg "Image from Wikimedia Commons, https://commons.wikimedia.org/wiki/File:Chinese_books_at_a_library.jpg")

# Contributions to LumoSQL Documentation are Welcome

The first rule of LumoSQL documentation is "Yes please, we'd be delighted to
receive patches and pull requests, in any way you want to make them". Anyone
who has gone to the trouble to write down something useful about LumoSQL is our
friend. We know there's a lot to fix. Here is [the TODO](./TODO.md).

If you want to make a quick documentation fix, then edit the Markdown and send
it to us by any means you like, especially a Github Issue or Pull Request. You
might just want to send us some improved paragraphs on their own. If this
sounds like you, stop reading now and get on with sending us text :-)

If you want to do something more serious with the documentation then you need
to read on, learning about our standards, recommended tools and processes. 

* The main website text, under the directory `doc/` .
** Images, such as PNG or JPEG format, stored in `doc/images`
** Images that are captured from videos and in the docs as thumbnails, also in `doc/images`

The Markdown files are standalone and complete - you can read them online just as they are.

Tables of contents are tricky, and covered below.

# LumoSQL Does Not Replicate Docs for Components such as SQLite, LMDB and more

LumoSQL Documentation is standalone in evey way, including formats, tools and standards.

However, LumoSQL documentation refers to and should be consulted together with the [SQLite
documentation](https://www.sqlite.org/docs.html), because with the following
exceptions, LumoSQL works (or should work) in exactly the same way as SQLite.
LumoSQL definitely not want to duplicate SQLite documentation, and regards the
excellent SQLite documentation as definitive except where indicated. 

Differences with SQLite arise:

* Where there is an extra/different storage backend to the SQLite Btree storage system
* Where there are extra parameters in the user interface (commandline, API, pragmas) for another backend
* When describing how the LumoSQL source tree works
* When LumoSQL is working as other than an embedded library
* When LumoSQL has an extra/different frontend to the SQLite SQL processor

It isn't only SQLite documentation that LumoSQL embraces. There is also [LMDB
Documentation](http://www.lmdb.tech/doc/), and more to come as LumoSQL integrates more
components. It is very important that LumoSQL not attempt to replicate these
other documentation efforts that are kept up to date along with the corresponding code.

# Text Standards and Tools

LumoSQL documentation will be written in [Fossil-compatible Markdown](https://fossil-scm.org/home/md_rules)
with few Fossil-isms except for [Pikchr](https://pikchr.org) blocks.

Text encoding will be [UTF-8](https://en.wikipedia.org/wiki/UTF-8) . Here is
one [expert anecdote about why UTF-8 matters](https://yihui.org/en/2018/11/biggest-regret-knitr/).

Versions of Pandoc earlier than 2.0 did not support Markdown well as an output format, and the 
Lua extension system was insufficient for LumoSQL's HTML generation needs.

# Diagram Standards and Tools

## LumoSQL Diagram Signature

The LumoSQL Diagram Signature is identical to the LumoSQL image signature. It should be 
placed on the bottom right hand corner of all diagrams created for LumoSQL, but not on
diagrams from other sources unless modified for LumoSQL.

   (TODO: Create a LumoSQL Diagram Signature using Pikchr :-) 

## Using the LumoSQL Diagram Library

The file images/lumo-diagram-library.md contains Pikchr primatives for the main
architectural elements of LumoSQL.  If you find that you need to add a new
element when making a diagram, you should also add it to this document.

The lumo-signature.md file is to be added to the base of all LumoSQL diagrams and images.
It contains the logo and copyright string.

   (TODO: Create lumo-diagram-library.md and lumo-signature.md ) 

## Diagram Style Guide

Colour palette: Friendly for high-contrast. See lumo-diagram-library.md for standard colours.
Fonts: See lumo-diagram-library.md

   (TODO: Complete when the diagram library is finished.)

# Image Standards and Tools

Images for LumoSQL documentation will be stored in /images/ and the
filenames should start with `lumo-` . PNG should be the default image format, 
followed by JPG. 

Include attribution in the alt-text tag. All images should have attribution,
even if the LumoSQL project provided them.  The caption should be left out if
the image is self-evident and the alt-text also explains what the image is, 
This example is approximately from the top of this chapter:

```
![Optional caption, eg "Chart of Badgers vs Profit"](./images/lumo-doc-standards-intro.jpg "Image from Wikimedia Commons, https://commons.wikimedia.org/wiki/File:Chinese_books_at_a_library.jpg")
```

# Previewing Markdown before Pushing

Lumodoc uses [Fossil embedded documentation](https://fossil-scm.org/home/doc/trunk/www/embeddeddoc.wiki). Fossil
allows preview of documentation before it is committed, like this:

<b>
```
    fossil ui --page doc/ckout/docdoc/README.md
```
</b>

# Copyright for LumoSQL Documentation

LumoSQL documentation is original and copyrighted under the 
[Creative Commons By-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/legalcode), 
except where indicated. Mostly it's better to link to the original, but if you
need to cite paragraphs of someone else's documentation then attribute, and if
more, check the license on the original.

The Creative Commons copyright applies to all LumoSQL documentation media.

Some documentation or media brings conditions of use with it, especially
attribution, and this must be respected.

# Metadata Header for Text Files

The first lines of all LumoSQL documentation files should always be something like this:

```
   <!-- SPDX-License-Identifier: CC-BY-SA-4.0 -->
   <!-- SPDX-FileCopyrightText: 2020 The LumoSQL Authors -->
   <!-- SPDX-ArtifactOfProjectName: LumoSQL -->
   <!-- SPDX-FileType: Documentation -->
   <!-- SPDX-FileComment: Original by Dan Shearer, 2020 -->
```

# Human Languages - 人类语言

English is currently the main documentation language. Others are welcome, and
not just as translations. For example, embedded SQL is particularly important
in China (due to the number of developers in China creating software containing SQLite for use 
both in China and worldwide) and we welcome original content. To make it feel welcoming, we have
tried to make all the illustrative images in LumoSQL have some kind of Chinese
and/or Mandarin context.

# Creating and Maintaining Table of Contents

LumoSQL had to make a decision about creating navigable ToC indexes. We would rather not 
write our own tools or scripts.

The problem we have is summarised in a [well-known Github bug report](https://github.com/isaacs/github/issues/215):

> When I see a manually generated table of contents, it makes me sad.
> When I see a huge README that is impossible to navigate without it, it makes me even sadder.
> LaTeX has it. Gollum has it. Pandoc has it. So why not [Fossil]?

Fossil [has made a decision](https://fossil-scm.org/forum/forumpost/cfec8933dc) not to support
tables of contents inline. That decision seems final.

**LumoSQL Decision as of March 2020**: ToC Markdown must appear in the raw markdown. That means a TOC
needs to be created and then inserted into the original source markdown file
rather than automatically generated as part of an online rendering process or offline pipeline.

**Non-markdown metadata won't work:** With Pandoc, when writing, say, a report
in Markdown, a tiny bit of metadata at the top of the file allows us to say
`\tableofcontents`  and `/usr/bin/pandoc` will then produce a beautiful PDF,
and also other formats such as HTML.  However, LumoSQL documentation needs to
be processed by renderers that are a lot less sophisticated than Pandoc,
including the Github markup processor. So we can't rely on metadata.

**Pandoc's Markdown output is improving but not yet good enough:** Pandoc can 
read Markdown and output Markdown, including a ToC.  A command such as 

```pandoc --standalone -f gfm -t gfm --toc -o lumo-output.md -i lumo-input.md```

is supposed to work and probably does, we just haven't seen it yet. Pandoc's Markdown
output used to be poor, but since version 2.0 is has improved a lot. Pandoc --toc is
hopefully the eventual answer, although as of 2.9 it doesn't seem to work at all, despite 
the documentation claiming it does.

**We are left with ad-hoc processing solutions for now:**

* There are also options for doing Markdown TOC in editors such as vim, for example [vim-markdown-toc](https://github.com/mzlogin/vim-markdown-toc)

* Editor.md, referred to in the "Previewing Markdown Before Pushing" section
above, will generate a table of contents where it sees the token `[TOC]` and a
dropdown index TOC menu where it sees `[TOCM`. However since the output is HTML
not markdown it is not so useful to LumoSQL (but it is very beautiful.)

# Tidying Markdown (mostly not required)

Tidying is about automatically adjusting the whitespace, pagebreaks and general formatting 
to be neat and consistent. But maybe you don't even need to, just write tidy 
text in the first place. 

If you want to clean up someone else's Markdown, then stop and ask first.
Automated cleanups and prettiers change hundreds of lines in a file without any
effect on the output, and that makes a diff impossible to review, effectively
rebasing it and destroying the history.

The documentation Makefile is not going to include any Markdown tidying because
of the potential for making things worse. As of version 2.0 Pandoc works better
for cleaning up markdown but isn't perfect. Parameters to experiment with include:

```
  -t gfm            (triggers a few defaults, including headers in ATX style)
  --wrap=preserve   (mostly limits changes to making headings ATX style)
  --columns=85      (stops most links breaking in editors doing syntax highlighting)
```
  
