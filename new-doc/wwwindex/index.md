---
title: LumoSQL Project Repositories
---

**Non-technical Introduction**

This is the home for the three [open source-licensed](https://license.lumosql.org) [LumoSQL](https://lumosql.org/src/lumosql/) repositories. LumoSQL is a modification of [SQLite](https://sqlite.org), the world's 
[most-used software](https://www.sqlite.org/famous.html), to 
add technical enhancements for performance, security and measurement. The modifications are done in cooperation with SQLite community and its twin project [Fossil](https://fossil-scm.org/).

LumoSQL is supported by [NLnet](https://nlnet.nl).

## LumoSQL Database Project

The [LumoSQL Database Project](https://lumosql.org/src/lumosql) builds modified
SQLite. The user can specify which version of SQLite is to have which features
added to it, and whether to benchmark the resulting binary. Features that can
be added to SQLite relate to different key-value storage backends, and
to security/integrity.

LumoSQL has code to:

* pull in multiple versions of SQLite, LMDB and BDB. We are also trying hard to get 21st-century K-V stores too, such as Adaptive Radix Trees and Fractal Trees
* combine these disparate trees to give a matrix of SQLite versions and backends, and versions of backends
* run [benchmarking](https://lumosql.org/src/lumosql/doc/trunk/doc/lumo-build-benchmark.md) of the matrix according to user-selected parameters, storing the results in an SQLite database
* assure data integrity. LumoSQL exposes data verfication mechanisms to end users, possibly the first SQL database to do so. Every row can be checksummed as it is written and verified as it is read. This is transparent to unmodified SQLite reading these databases, and works with new K-V store backends

LumoSQL Database preview version 0.4 [was released](https://lumosql.org/src/lumosql/doc/trunk/doc/release-announce-0.4.md) on 2021-01-10 .

## LumoSQL Documentation Project

The [LumoSQL Documentation Project](https://lumosql.org/src/lumodoc/doc/trunk/README.md) contains:

* The goals and technical details for the LumoSQL database
* A roadmap for the evolution of LumoSQL, towards new stable SQLite APIs
* Plans for new features for LumoSQL, such as per-row checksums
* Research on related codebases, mapping out the ecosystem of SQLite forks and other code
* Papers related to SQLite benchmarking, tuning and more

## The Not-Forking Tool

 [The Not-Forking Tool](https://lumosql.org/src/not-forking) is how LumoSQL
combines codebases with minimal disruption. The ultimate goal is is to have a
stable storage backend API in SQLite, but to develop that we need to see the
codebases joined together, and to understand 20 years of closely-coupled
history in SQLite internals. Not-forking has allowed us to work with multiple
different versions of SQLite, LMDB and BDB without having to maintain ports or
APIs. Not-forking is relevant to any project that needs to keep in synch with
multiple upstreams each with multiple versions, whether  available via Git,
tarball or Fossil.

SQLite is conservative about breaking compatibility due to its immense
userbase, but LumoSQL can apply new features without forking SQLite thus
getting the best of both worlds. SQLite can see alternate futures, while
LumoSQL is not carrying the burden of forking.


--------------------------

## The LumoSQL Archives of Dead Code

[Archive 2: Early LumoSQL on Fossil](https://lumosql.org/src/archive2-lumosql-on-fossil/timeline)
has lots of experimentation, dead-ends and more. It was imported from GitHub, and 
that sparked some [Fossil development](https://fossil-scm.org/forum/forumpost/92db82a45e?t=h) because
once upon a time a previous SQLite Fossil had been imported into an upstream. This archive also
was the last time LumoSQL was a monolithic project.

[Archive 1: Early LumoSQL on Github](https://github.com/LumoSQL/archive1-LumoSQL-on-github) has the
very earliest work including excavations of ancient code. All the Gihub issues from this project have been moved to the
current LumoSQL fossil archive, or wiki pages, or otherwise dealt with. 
