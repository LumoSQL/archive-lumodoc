# Contributing to the LumoSQL Documentation Project

This is not the [LumoSQL project][lumo], it is the separate **LumoSQL Documentation Project**.

If you wish to make any changes to [the LumoSQL Documentation project’s files][lumodoc], 
this is how you get started with handling the files. For the details of LumoSQL 
documentation standards and tools, see [the Documentation Handbook](https://lumosql.org/src/lumodoc/doc/trunk/docdoc/README.md).

We try to keep the barriers to contribution low, which is assisted by
our decision to use [Fossil].

If you are familiar with Fossil, you will be able to start editing
documentation straight away. The rest of this document has useful non-technical
information about contributing too.

***NOTE! FIXME This document has not yet been fully converted from its orginal over in LumoSQL***

[lumo]:[https://lumosql.org/src/lumosql]
[lumodoc]:[https://lumosql.org/src/lumodoc]
[testbuild]: https://lumosql.org/src/lumosql/doc/tip/doc/lumo-test-build.md


## <a id="ghm"></a> The GitHub Mirror Is One-way

The LumoSQL Documentation [Fossil] repository is the official home for
this project. This is where the action is, and although you 
can raise PRs on Github for us to feed through Fossil, or send us patches,
do consider joining us on Fossil. At least on the forum.

If you want an exact clone of the LumoSQL Documentation Project repo, or if you
wish to contribute to the project’s development with full credit for your
contributions, it’s best done via Fossil, not via GitHub.

[Fossil]: https://fossil-scm.org/


## <a id="gs-fossil"></a> Getting Started with Fossil

The LumoSQL software project is hosted using the Fossil
[distributed version control system][dvcs], which provides most of the
features of GitHub without [the complexities of Git][fvg].

Those new to Fossil should at least read its [Quick Start Guide][fqsg],
followed by [the official Fossil docss][fdoc]. You can download
[precompiled binaries][fbin] or [install from source](bffs); either way, make 
sure you have Fossil 2.14 or higher.

If you have questions about Fossil, ask on [the Fossil forum][ffor].

[bffs]:   https://fossil-scm.org/home/doc/trunk/www/build.wiki
[fbin]:   https://fossil-scm.org/index.html/uv/download.html
[fvg]:    https://fossil-scm.org/home/doc/trunk/www/fossil-v-git.wiki
[dvcs]:   https://en.wikipedia.org/wiki/Distributed_revision_control
[fdoc]:   https://fossil-scm.org/home/doc/trunk/www/permutedindex.html
[ffor]:   https://fossil-scm.org/forum/
[fqsg]:   https://fossil-scm.org/home/doc/trunk/www/quickstart.wiki


## <a id="fossil-anon" name="anon"></a> Fossil Anonymous Access

The fossil clone command has the same syntax as git:

    $ fossil clone https://lumosql.org/src/lumodoc
    $ cd lumosql

but if we create a particular directory structure then Fossil can be used for
its strengths, as we show in later sections of this document:

    $ mkdir -p ~/docsrc/lumodoc-trees
    $ cd ~/docsrc/lumodoc-trees
    $ fossil clone https://lumosql.org/src/lumodoc
    $ cd lumodoc

That results in a clone of the `lumodoc.fossil` repository plus a check-out
of the current trunk in a `lumodoc/` directory alongside it, both of them
underneath `lumodoc-trees`. 

Once you have done this, you will just be working with the cloned repository.

You only need to do this once per machine. 

## <a id="login"></a> Fossil Developer Access

If you have a developer account on the `lumosql.org/src/lumodoc` Fossil
instance, just add your username to the URL like this:

    $ fossil clone https://USERNAME@lumosql.org/src/lumodoc

If you’ve already cloned anonymously, simply tell Fossil about the new
sync URL instead:

    $ cd ~/docsrc/lumosql/trunk
    $ fossil sync https://USERNAME@lumosql.org/src/lumosql

Either way, Fossil will ask you for the password for `USERNAME` on the
remote Fossil instance, and it will offer to remember it for you. If
you let it remember the password, operation from then on is almost the
same as working with an anonymous clone, except that on checkin,
your changes will be sync’d back to the repository on lumosql.org if
you’re online at the time, and you’ll get credit under your developer
account name for the checkin.

If you’re working offline, Fossil will still do the checkin locally, and
it will sync up with the central repository after you get back online.
It is best to work on a branch when unable to use Fossil’s autosync
feature, as you are less likely to have a sync conflict when attempting
to send a new branch to the central server than in attempting to merge
your changes to the tip of trunk into the current upstream trunk, which
may well have changed since you went offline.

You can purposely work offline by disabling autosync mode:

    $ fossil set autosync 0

Until you re-enable it (`autosync 1`) Fossil will stop trying to sync your
local changes back to the central repo.  We recommend disabling autosync mode
only when you are truly going to be offline and don’t want Fossil attempting to
sync when you know it will fail.


## <a id="gda"></a> Getting Document Commit Access

We are pretty open about giving commit rights to the documentation tree. Bear in mind
the forum also supports Markdown, so that's also a good way to start scratching a 
document together.

One way to get developer access is to provide one good, substantial [patch](#patches) 
to LumoSQL documentation. If we’ve accepted one of your patches, we will listen when you ask for a 
developer account.

If you have other ways of contributing then you should also get in touch. Documentation patches 
are not the only kind of contribution, although they are the main one.

Documentation isn't code (well, there's a little code in this tree but that's not the
main point.) Due to that, and because everything is kept versioned in Fossil anyway,
we tend just to commit directly to the project's main branch, called "trunk".

## <a id="forum"></a> Developer Discussion Forum

The “[Forum][pfor]” link at the top of the Fossil web interface is for
discussing LumoSQL documentation development and LumoSQL generally.  You can sign up for the
forums without having a developer login, and you can even post anonymously. If
you have a login, you can [sign up for email alerts][alert] if you like.

Keep in mind that posts to the Fossil forum are treated much the same
way as ticket submissions and wiki articles. They are permanently
archived with the project. The “edit” feature of Fossil forums just
creates a replacement record for a post, but the old post is still
available in the repository. Don’t post anything you wouldn’t want made
part of the permanent record of the project!

[pfor]: https://lumosql.org/src/lumodoc/forum
[alert]: https://lumosql.org/src/lumodoc/alerts


## <a id="patches"></a> Submitting Patches

If you do not have a developer login on the LumoSQL repository,
you can still send changes to the project.

The simplest way is to say this after developing your change against the
trunk of LumoSQL:

    $ fossil diff > my-changes.patch

Then either upload that file somewhere (e.g. Pastebin) and point to it
from a [forum post][pfor] . You will need to declare you are using the
LumoSQL licence. 

If your change is more than a small patch, `fossil diff` might not
incorporate all of the changes you have made. The old unified `diff`
format can’t encode branch names, file renamings, file deletions, tags,
checkin comments, and other Fossil-specific information. For such
changes, it is better to send a Fossil bundle:

    $ fossil set autosync 0                # disable autosync
    $ fossil checkin --branch my-changes
      ...followed by more checkins on that branch...
    $ fossil bundle export --branch my-changes my-changes.bundle

After that first `fossil checkin --branch ...` command, any subsequent
`fossil ci` commands will check your changes in on that branch without
needing a `--branch` option until you explicitly switch that checkout
directory to some other branch. This lets you build up a larger change
on a private branch until you’re ready to submit the whole thing as a
bundle.

Because you are working on a branch on your private copy of the
LumoSQL Fossil repository, you are free to make as many checkins as
you like on the new branch before giving the `bundle export` command.

Once you are done with the bundle, send it to the developers the same
way you should a patch file.

If you provide a quality patch, we are likely to offer you a developer
login on [the repository][repo] so you don’t have to continue with the
patch or bundle methods.

Please make your patches or experimental branch bundles against the tip
of the current trunk. PiDP-8/I often drifts enough during development
that a patch against a stable release may not apply to the trunk cleanly
otherwise.

[repo]:  https://lumosql.org/src/lumosql


## <a id="code-style"></a> LumoSQL Coding Rules

Style Guide Goes here...

