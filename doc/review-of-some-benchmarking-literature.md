Benchmarking LumoSQL
====================

## Benchmarking is Hard

So why not seek advice from people who have studied it.

This document includes the recommendations of the 2018 paper 
[Fair Benchmarking Considered Difficult: Common Pitfalls In Database Performance Testing](https://mytherin.github.io/papers/2018-dbtest.pdf). 
This is in the context of the [Dangers and Complexity of Sqlite3 Benchmarking](https://www.cs.utexas.edu/~vijay/papers/apsys17-sqlite.pdf) paper referred to elsewhere.
Other searches were done, but this is not the slightest bit exhaustive.

## Limiting the Problem Space

Fortunately LumoSQL has some advantages that reduce the problem space for benchmarking:

* *we are making benchmarking runs unique and persistent*. That means we don't have 
to keep re-running the same results time and again, and that people can contribute 
results from their different environments which, if they all agree, lets us discount 
some entire dimensions of possible optimisations.
* *We are only modifying the bottom layer*. The test harness is effectively the entire SQLite stack above the btree layer
(or lumo-backend.c when we implement it). SQLite benchmarking is difficult because
there are so many pragmas and compile options, but most of these apply to all
backends. The *effect* of a given pragma or compile option may differ by
backend, but we hope this will be a lesser, second-order effect. It might not be.
* *backends today differ in relatively dimensions* despite being very different
MVCC K-V stores. We need to document the special tuning parameters for each of the backends,
and there are still major differences especially in locking. And LMDB 1.0rc1 has page-level 
crypto. But its not like we have a LSM backend or a distributed backend. Not yet.
* *No networking, clustering or client interoperability*. Not yet.
* *Not across multiple platforms*. Not yet. We will be though. Which will be a challenge
for the benchmarking suite. And in getting the dimensions right, because different OSs
have different specialities. Android and iOS tuning will be particularly important.

# Nature of the Benchmarking

The SQL benchmarking is to seek answers about throughput:

* total time elapsed for tests
* bytes per second (in cases where we are reading or writing a known quantity of data)
* operations per second (with the ops measured either by *vdbe*c, or os_*c, or both.) 

LumoSQL benchmarking will mostly be using blackbox testing approaches
(high-level functionality) with some highly-targetted whitebox testing for
known tricky differences between backends (eg locking). 

Being a low-level library, functional benchmarking often gets close to
internals testing. That's ok, but we need to be aware of this. We don't want to
be doing internals testing. That is for make test.

At a later date we can add benchmarking at LumoSQL KV API level, ie
lumo-backend.c .  This is so that we can observe if the performance of each
backend remains roughly the same (especially, *relatively* the same compared to
the others) whether accessed via the SQLite API or directly via the common KV
API. It is possible that the SQLite stack will have some unexpected interaction
with a particular backend - to pick a pathological corner case, a magic string.

# Configuration Sets

For each benchmarking run this what is meant by a "configuration set": [... TBD extract from paper]

# Checklist from the "Considered Difficult" Paper

[TBD incomplete...]

We have considered the checklist given at the end of the "Considered Difficult" paper in the context
of repeated runs of SQLite workloads with different backends.

We have not as-yet really started getting into this checklist. 

* Choosing your Benchmarks.
  - Benchmark covers whole evaluation space
  - Justify picking benchmark subset
  - Benchmark stresses functionality in the evaluation space
* Reproducible by publishing:
  - Hardware configuration
  - DBMS parameters and version
  - Source code or binary files
  - Data, schema & queries•Optimization.
  - Compilation flags
  - System parameters
* Apples vs Apples
  - Similar functionality
  - Equivalent workload
* Comparable tuning
  - Different data
  - Various workloads
* Cold/warm/hot runs.
  - Differentiate between cold and hot runs
  - Cold runs: Flush OS and CPU caches
  - Hot runs: Ignore initial runs
* Preprocessing.
  - Ensure preprocessing is the same between systems
  - Be aware of automatic index creation
* Ensure correctness.
  - Verify results
  - Test different data sets
  - Corner cases work
* Collecting Results.
  - Do several runs to reduce interference
  - Check standard deviation for multiple runs
  - Report robust metrics (e.g., median and confidence inter-vals)


# Possible Benchmarking Dimensions

[TBD - notes only]

* Dataset can fit entirely in memory (or not)
* Caching (durability on/off)
* Updates vs Reads vs -Only
* Ops per second at disk
* VDBE ops per second
* Latency at C API
* Blobs

# SQL Dimensions

* Single filtering plus offset
* join with grouping and ordering
* multiple indexing

# Concurrency Dimensions

This is going to be very important, especially since concurrency is one of SQLite known weak points.
[The async SQLite tests](https://github.com/sqlite/sqlite/blob/master/test/async2.test) don't seem to be stressing concurrency really.
[mptest](https://github.com/sqlite/sqlite/tree/master/mptest) seems to be more along those lines but I haven't done sample runs of it (mptest hasn't changed in 7 years, and all the references to it seem to be in the context of Windows, if that means anything.)

# Workload Simulation

* Analytics-type workload patterns
* Human thread-following app simulation - nearly all read operations
* 50/50 read/write - classical ecommerce-type application
* Mixture of all of above on different threads to be really mean

# Missing Items

* [HammerDB](https://github.com/TPC-Council/HammerDB) should be ported to SQLite. SQlite is *used* by HammerDB but is not a target database.
