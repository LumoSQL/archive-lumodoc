<!-- SPDX-License-Identifier: CC-BY-SA-4.0 -->
<!-- SPDX-FileCopyrightText: 2020 The LumoSQL Authors -->
<!-- SPDX-ArtifactOfProjectName: LumoSQL -->
<!-- SPDX-FileType: Documentation -->
<!-- SPDX-FileComment: Original by Dan Shearer, 2020 -->


Table of Contents
=================

   * [Table of Contents](#table-of-contents)
   * [About Benchmarking](#about-benchmarking)
   * [All SQLite Performance Papers are Nonsense](#all-sqlite-performance-papers-are-nonsense)
   * [Limiting the Problem Space](#limiting-the-problem-space)
   * [What Questions Will Benchmarking Answer?](#what-questions-will-benchmarking-answer)
   * [Details of Benchmarking Code](#details-of-benchmarking-code)
      * [Metrics](#metrics)
      * [SQL in benchmark.tcl](#sql-in-benchmarktcl)
      * [SQL Logic Test](#sql-logic-test)
      * [C speed tests with SQLite C API](#c-speed-tests-with-sqlite-c-api)
   * [Computer architectures and operating systems](#computer-architectures-and-operating-systems)
      * [C speed tests with the SQLite/LumoSQL KV API](#c-speed-tests-with-the-sqlitelumosql-kv-api)
   * [List of Relevant Benchmarking and Test Knowledge](#list-of-relevant-benchmarking-and-test-knowledge)

About Benchmarking
==================

The [LumoSQL project aims](./lumo-project-aims.md) include:

> A Privacy-compliant Open Source Database Platform with Modern Design and Benchmarking.

LumoSQL is a modification of SQLite that adds multiple API-similar storage
backends. Benchmarking is quantitive measurement that tell us how these 
backends perform in particular circumstances.

The strange thing is that benchmarking between SQL databases is almost non-existant, as well as difficult.

We focus on the practical recommendations of the 2018
paper [Fair Benchmarking Considered Difficult:Common Pitfalls In Database Performance Testing](https://mytherin.github.io/papers/2018-dbtest.pdf). 
We store the results in an SQLite database, and we make the method and the 
results available publicly.

The LumoSQL benchmarking problem is less difficult than comparing 
unrelated databases, which is perhaps why the [Transaction Processing Performance Council](https://tpc.org) has not published news since 2004.
There are testing tools released with SQLite, Postgresql, MariaDB etc, but 
there simply is no way to compare. Benchmarking and testing overlap.

The well-described [testing of SQLite](https://sqlite.org/testing.html)
involves some open code, some closed code, and many ad hoc processes. Clearly
the SQLite team have an internal culture of testing that has benefitted the
world. However that is very different to testing that is reproducible by
anyone, which is in turn very different to reproducible reproducible by anyone,
and that is even without considering whether the benchmarking is a reasonable
approximation of actual use cases.

# All SQLite Performance Papers are Nonsense

In 2017 a helpful paper was published by [Purohith, Mohan and Chidambaram](https://www.cs.utexas.edu/~vijay/papers/apsys17-sqlite.pdf) on the
topic of "The Dangers and Complexities of SQLite Benchmarking". Since the first
potential problem is that this paper itself is in error, LumoSQL repeated
the literature research component in the paper. We agree with the authors in stating:

> When we investigated 16 papers from the 2015-2017
> whose evaluation included SQLite, we find that none report
> all the parameters required to meaningfully compare
> results: ten papers do not report any parameters [17–26],
> five do not report the sync mode [27–31], while only
> one paper reports all parameters except write-ahead log
> size [32]. Without reporting how SQLite was configured,
> it is meaningless to compare SQLite results.

LumoSQL found three additional papers published in 2017-2019, with similar flaws.
In brief:

> **All published papers on SQLite's performance are nonsense**

And this is for SQLite alone, something that has relatively few parameters
compared to the popular online SQL databases. The field of SQL databases in
general is even more poorly benchmarked.

Benchmarking between SQL databases hardly exists at all. 

# Limiting the Problem Space

LumoSQL has some advantages that reduce the problem space for benchmarking:

* The test harness is effectively the entire SQLite stack above the btree layer
(or lumo-backend.c). It is true that SQLite benchmarking is difficult because
there are so many pragmas and compile options, but most of these apply to all
backends. The *effect* of a given pragma or compile option may differ by
backend, but this will be a second-order effect and hopefully not as severe as
first-order effects.
* The backends we have today differ in a relatively small number of dimensions,
usually to do with their speciality. The SQLite Btree backend has options for
WAL files, journals and cache sizes; the LMDB backend uses the OS buffer cache
and so there are OS-level defaults to be aware of; the BDB backend has tuning
options relating to cache and locking. That relatively small number of
differences still potentially gives a large benchmarking matrix, so we have to
control for that (or regard computation as free, which is close to accurate at
the scale of the LumoSQL project.)
* No networking, clustering or client interoperability involved. This
eliminates many classes of complexity.

To further reduce the problem space we will not be testing across multiple
platforms. This can be addressed later.

# What Questions Will Benchmarking Answer?

Questions by LumoSQL/SQLite internals developers:

- I am considering a change to the main code path to integrate a new feature,
  will the performance of LumoSQL suffer?
- I have identified a potential optimisation, is the performance benefit worth
  the additional complexity?
- I have implemented a new backend, should we make it the default?

Questions by LumoSQL/SQLite application developers:

- Is LumoSQL any different from SQLite when configured to use the SQLite backend?
- I have these requirements for a system, which LumoSQL backend should I choose?

# Details of Benchmarking Code

## Metrics

Benchmarking will take place via SQL, with these items being measured at least:

* Elapsed time for a series of SQL statements

  The TCL script benchmark.tcl is a forked version of speedtest.tcl, which 
  writes results to an SQLite database as well a producing HTML output.
  The SQL statements are discussed further down in this section. Each of the 
  timed tests will also have VDBE ops and IOPS recorded as per the next 
  two sections.

* VDBE Operations per second 

  benchmark.tcl can collect VDBE ops, but only with some help from LumoSQL.

  A timer is started in sqlite3_prepare(), VDBE opcodes are counted in
  sqlite3VdbeExec(), and the timer is stopped in sqlite3_finalize(). This
  then allows us to calculate how long the sql3_stmt took to execute per
  instruction. The number of instructions will be the same for all backends.

* Disk Operations per second

  benchmark.tcl can do this by comparing per-pid IOPS using the algorithm
  here: https://github.com/true/aspersa-mirror/blob/master/iodump . 
  We look up the IOPS at the beginning and end of the test and store the 
  difference. 

  This is not portable to other operating systems, however, that will
  hopefully be a relatively small variable compared to the the 
  variable of one backend vs another. 

## SQL in benchmark.tcl 

To start with we are modifying speedtest.tcl as described. We are adding a BLOB
test with large generated blobs, but it is basically the same. In the future we
need to have more realistic SQL statements. And that varies by use case:

1. embedded style SQL statements, typically developing for heavily resource
   constrained deployments, who are likely to use SQL to simply store and
   retrieve values and be more interested in tradeoffs and settings that
   reduce latency. Tightly coupled with the SQLite library. Short transactions.
2. online style SQL statements, used for transaction processing. Concurrency
   matters. Same SQL might be used with another database. Some long transactions.
3. online style SQL statements, used for analytics processing. Much more 
   batch oriented. Same SQL might be used with another database. Some long transactions.

## SQL Logic Test

It isn't clear that the SQL logic test is suitable for benchmarking. We are 
working on this, but our hope is that it will be readily adapatable.

[wiki]: https://www.sqlite.org/sqllogictest/doc/trunk/about.wiki
[fossil repository]: https://www.sqlite.org/sqllogictest/dir?name=src&type=tree
[results]:
  https://www.sqlite.org/sqllogictest/wiki?name=Differences+Between+Engines

This works by ODBC - noting that SQLite has an ODBC driver.

## C speed tests with SQLite C API

We have only done basic testing to make sure the code runs.  Our objective in
running these tests will be to quantify performance. These tests use the C API.

`speedtest1.c` appears to be very actively maintained by <https://sqlite.org>,
the file has a number of different contributors and has frequent commits.

`mptest.c` and `threadtest3.c` look promising for testing async access. See the 
notes previously about the unsophisticated concurrency handling we have already
demonstrated in SQLite. 

# Computer architectures and operating systems

We are not going to get ambitious with platforms and variations. For the present,
benchmarking on 64 bit x86 Linux will be sufficient.

We will impose memory pressure in benchmarking runs by limiting the memory
available to the LumoSQL process. However we can do this effectively with the
cgroups API rather than having small VMs.

Other obvious variations for the future include Windows, and 32-bit hardware.
We are ignoring these for now.

## C speed tests with the SQLite/LumoSQL KV API

This is a lesser priority.

It is important to also benchmark at the LumoSQL KV API level, ie
lumo-backend.c .  This is so that we can observe if the performance of each
backend remains roughly the same (especially, *relatively* the same compared to
the others) whether accessed via the SQLite API or directly via the common KV
API. It is possible that the SQLite stack will have some unexpected interaction
with a particular backend - to pick a pathological corner case, a magic string.

# List of Relevant Benchmarking and Test Knowledge

There is a section in the [Full Knowledgebase Relevant to LumoSQL](./lumo-relevant-knowledgebase.md) on benchmarking. 

