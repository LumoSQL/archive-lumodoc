<!-- SPDX-License-Identifier: CC-BY-SA-4.0 -->
<!-- SPDX-FileCopyrightText: 2020 The LumoSQL Authors -->
<!-- SPDX-ArtifactOfProjectName: LumoSQL -->
<!-- SPDX-FileType: Documentation -->
<!-- SPDX-FileComment: Original by Dan Shearer, 2020 -->


LumoSQL
=======

![](./images/lumo-logo-temp.svg "LumoSQL logo")


Table of Contents
=================

Welcome to the LumoSQL project, which builds on the excellent
[SQLite](https://sqlite.org/) project without forking it.  LumoSQL is an SQL database
which can be used in embedded applications identically to SQLite, but also
optionally with different storage backends and other additional behaviour.
LumoSQL emphasises benchmarking, code reuse and modern database implementation.

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


