---
title: "Handy Commands"
---
 
 See the size of partitions: 
 	df -h  
 		(-h stands for human-readable. It applies to 'ls' too)
 See the dependency of a package: 
 	apt-cache depends <package name>
 See the packages which are depndent on a package (reverse-dependency)
 	apt-get rdepends <package-name>
 Search for a package or metapackage: 	
 	aptitude search <search_string>
 See the list of open files:
 	lsof
