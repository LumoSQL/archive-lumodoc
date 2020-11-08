# Lumodoc, the LumoSQL Documentation Project

This is the project that maintains the documentation for
[LumoSQL](https://lumosql.org/src/lumosql). LumoSQL enhances the
[SQLite](https://sqlite.org) database library 
[without forking it](https://lumosql.org/src/not-forking).

***Lumodoc*** is a [Science Communication](https://en.wikipedia.org/wiki/Science_communication) project,
discussing the computer science, mathematics and human factors to do with ***LumoSQL***.
The software engineering project ***LumoSQL*** has created a new kind of database.

Lumo**SQL** and any other project wanting to link to the LumoSQL docs need to point at the 
"doc" directory within the Lumo**doc** project using this URL: 
[https://lumosql.org/doc](https://lumosql.org/doc). That is the finished product.
The README.md document you are reading is part of the Lumodoc project, not the finished product
Lumodoc produces, and the master version is kept at
[https://lumosql.org/src/lumodoc/](https://lumosql.org/src/lumodoc/) . The documentation
for the Lumodoc project is [in the "docdoc" directory](https://lumosql.org/src/lumodoc/dir?name=docdoc)
because it is documentation about documentation.

The list of jobs is in the [LumoDoc ToDo long-running forum thread](https://lumosql.org/src/lumodoc/forumpost/8b2baecc9f).

## Version Control and Website

Lumodoc sources and the official website are managed using the
[Fossil](https://www.fossil-scm.org/)[SCM](https://en.wikipedia.org/Source_control_management). 
If you are reading this on Github or anywhere other than <tt>lumosql.org</tt> then you are 
looking at a read-only mirror. Mirrors are good and important, but everything else in this 
project assumes you are working with the master repository for Lumodoc, hosted at lumosql.org.

## Contributing

Drop in to the [Lumodoc forum](https://lumosql.org/src/lumodoc/forum) and post a message
about what you think needs done. You can tell us about corrections to the documentation,
or contribute anything else you wish, noting that the forum understands the Markdown format.
You can [subscribe to email alerts](https://lumosql.org/src/lumodoc/alerts) for when there
has been a commit to the repository, or to get copies of all forum posts as email.

If you want to get more serious we recommend you 
[download Fossil or build it](https://fossil-scm.org/home/doc/trunk/www/build.wiki) on your 
local computer. Then run:

```
fossil clone https://lumosql.org/src/lumodoc
```

which will download the Fossil repository into lumodoc.fossil, create a directory called "lumodoc",
and then open the new local repository into that directory. You won't be able to push your 
commits back up to the central lumodoc repository without a username and password, but otherwise
you have everything you need to play around with the documentation tools. 

Try this for a start:

```
fossil ui
```

# Technical Implementation

The URL https://lumosql.org/doc is an Apache webserver alias pointing to the Fossil repository
directory [https://lumosql.org/src/lumodoc/doc](https://lumosql.org/src/lumodoc/doc). 
Fossil serves up the current version of the requested file, processing all markup according to 
[Fossil's Markdown rules](https://fossil-scm.org/home/md_rules), and generating HTML. The
HTML is then served by Apache just as if it was contained in my-webpage.html .

With the Markdown text, diagrams are specified using 
[Pikchr](https://pikchr.org/home/doc/trunk/doc/examples.md), a plain text format that generates SVG.

In a near-future version of the Lumodoc project it is almost inevitable that we will change this
workflow to include the amazing [Pandoc](https://pandoc.org) document convertor. The first step
to using Pandoc would be to have it process the Markdown files and generate new Markdown files
that include a table of contents (all ToCs are currently generated by a tool and imported manually.)
Pandoc can convert from Markdown to PDF and HTML, so there are many other eventual possibilities.

## Really Why a Separate Project?

In more detail... while there are a few very code-specific technical documents
included in the main LumoSQL project, everything else is here because:

* Document management tools, scripts and work-in-progress notes are nothing to do with a production database system and shouldn't be mixed up with it
* Other output formats such as a website(s) or a book are even further from a production database
* Documentation often has a very different release cycle and management process than code
* Bugs, fixes and complaints to documentation shouldn't generally be mixed up with code problems
* Everthing in LumoSQL is under [one single code-specific licence](https://lumosql.org/src/lumosql/LICENCES/README.md) , whereas here in Lumodoc we mainly use [a documentation-specific licence](LICENCES/README.md).

Co-incidentally, 
[SQLite documentation](https://www.sqlite.org/docsrc/doc/trunk/README.md) is also
managed in a separate repository. This is one of many examples where the
LumoSQL project is somewhat similar to SQLite.


