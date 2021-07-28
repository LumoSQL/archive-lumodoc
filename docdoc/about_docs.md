
# Table of Contents

* [Why Choose LumoSQL](./1.1-front-page.md)
	* [Top Features](./1.2-top-features.md)
	* [Performance](./1.3-performance.md)
	* [Get LumoSQL](./1.4-install-LumoSQL.md)
* How LumoSQL Works
	*[Features](./2.2-features.md)
		* [API](./api.md)
		* [Virtual Machine Layer](./virtual-machine.md)
		* [Savepoints](./what-are-savepoints.md)
		
		* [Encryption](./encryption.md)
		* [BDB Backend](./backends.md)
		* [Rollback](./WALs.md)	
		* [Corruption Detection](./lumo-corruption-detection-and-magic.md)	
		* [Online Database Servers](./online-database-servers.md)
		
	* [SQLite-LumoSQL Comparison](./2.3-SQLite-Lumo-comparison.md)
	* [Relevant Knowledgebase](./2.4-relevant-knowledgebase.md)
* Development
	* [Contribure to LumoSQL](./3.1-contributions.md)
	* [Legal Aspects](./3.2-legal-aspects.md)
	* [Benchmarking](./3.3-benchmarking.md)
	* [Not-Forking Tool](./3.4-not-forking-tool.md)
	* [Test Build](./3.5-lumo-test-build.md)
	* [Developement Landscape](./3.6-development-notes.md)
	* [Relevant Codebases](./3.7-relevant-codebases.md)
	* [Timeline](./3.8-timeline.md)


Selling Points
====================================================

1.1-front-page.md 
.
add pictures, bullet list


1.2-top-features.md 
.
copied from aims, change will to has and add links to full information to section 2


1.3-performace.md 
.
discussion on speed and benchmark results page 


1.4-install-LumoSQL.md 
.
from quickstart
only on how to get packages for sqlite3


How LumoSQL Works
==================================================


2.2-features.md 
.
introduction and list of features and changes to SQLite:
api.md
virtual-machine.md
what-are-savepoints.md
encryption.md (needs a more specific description when implemented)
backends.md 
WALs.md
lumo-corruption-detection-and-magic.md 
online-database-servers.md


2.3-SQLite-Lumo-comparison.md 
.
take from implementation and from aims , summary of differences between SQLite and Lumo (very incomplete)


2.5-relevant-knowledgebase.md 
.
different chapters to be linked to benchmarking, encryption ...

Development
==================================================

3.1-contributions.md 
.
text from https://lumosql.org/src/lumodoc/doc/trunk/README.md


3.2-legal-aspects.md 
.
copy of legal aspects

3.3-benchmarking-how-to.md
from install, instructions how to perform benchmarking and some results from the past (NEW: currently incomplete)

3.3-benchmarking.md 
.
copy of benchmarking and benchmarking literature
fix the end
discussion section


3.4-not-forking-tool.md 
.
copy of not-forking
.#git has info about git shouuld be deleted 
(add this https://lumosql.org/src/not-forking/doc/trunk/README.md)

3.5-lumo-test-build.md 
.
copy of test build


3.6-development-landscape.md 
.
currently copy of lumo-landscape
aims, planning, progress of the project

3.7-relevant-codebases.md 
.
copy of codebases
link to encryption, BDB, networking, benchmarking


3.8-timeline.md 
.
put links to the timeline pages 
