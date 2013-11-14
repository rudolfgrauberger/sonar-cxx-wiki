Here is a quick guide how to run the supported analyzers and generate reports such that it fits SonarQube's needs.

### Cppcheck

In order to run Cppcheck and generate a fitting report, make sure:

* to pass all include directories (using _-I <path>_) as otherwise the analysis will be incomplete
* that the <sources> parameter matches the **sonar.sources** list in _sonar-project.properties_
* to create a XML-report 'version 1' using the parameters ```--xml --xml-version=1```
* to get the report from the standard error channel

Example command line:

```BASH
cppcheck -v --enable=all --xml --xml-version=1 -I<include directory> <sources> 2> report.xml
```
 
A Cppcheck run may take a while on a big code base. To cut down analysis times, check the following options:

* Use ```-j N``` option to run _N_ workers in parallel
* Use only checks you're interested in via the option ```_--enable=<check>_```
* Restrict checking of preprocessor configurations using the options ```-D -U```
* Get a faster machine ;)
 
Rule Extensions
Icon
To extend the set of known Cppcheck rules define them in the file $SONARQUBE_HOME/extensions/rules/cppcheck. See Extending rules in C++ analysers for details.

Valgrind
SonarQube can be fed with results of a Valgrind/Memcheck analysis. That's very valuable because:
due to its dynamic nature, the false positives rate is very low (Given good maintained suppression files, of course) 
it is able to find serious issues which are often hard to detect otherwise
Just tell Valgrind to generate XML output. The 'tool' option isn't necessary as 'memcheck' is the default one. Make sure the binaries contain debug info.
valgrind --xml=yes --xml-file=report.xml <program> <arguments>
Rule Extensions
Icon
To extend the set of known Vagrind rules define them in the file $SONARQUBE_HOME/extensions/rules/valgrind. See Extending rules in C++ analysers for details.
Vera++
Vera++ does static C++ code checking, focusing mostly on style issues.
To feed Vera++ analysis results into SonarQube:
Find all the files we want to be analysed
Pipe this list into Vera++ and 
Pipe the resulting output into a Perl script which finally generates the required XML. 
find <path> -regex ".*\.cc\|.*\.hh" | vera++ - -showrules -nodup |& vera++Report2checkstyleReport.perl > report.xml
Rule Extensions
Icon
To extend the set of known Vera++ rules define them in the file $SONARQUBE_HOME/extensions/rules/vera++. See Extending rules in C++ analysers for details.
RATS
RATS stands for "Rough Auditing Tool for Security". This tool performs static C++ code checks focusing mainly on security issues. Just tell it to create XML output and redirect the standard channel into a file.
rats -w 3 --xml <sources> > report.xml
Rule Extensions
Icon
To extend the set of known RATS rules define them in the file $SONARQUBE_HOME/extensions/rules/rats. See Extending rules in C++ analysers for details.

Pc-Lint
The Pc-Lint XML output needs to be formated to fit SonarQube.
// XML options for SONAR.
-v // Turn off verbosity
-width(0,0) // Don't break long lines
+xml(?xml version="1.0" ?) // add version information
+xml(results) // Turn on XML escapes
-"format=<issue file =\q%f\q line = \q%l\q number = \q%n\q desc = \q%m\q/>"
-"format_specific= "
-hFs1 // The height of a message should be 1 i.e. don't output the line in error
-e900 // 'Successful completion message' confuses ALOA
This formating has been verifed with Pc-Lint 9.0i.
For further details on how to configure Pc-Lint please refer to product page (Official Site)
Icon
Rules for this tool are disabled by default, so they need to be enabled in the relevant quality profile before they can be imported into SonarQube
Rule Extensions
Icon
To extend the set of known Pc-Lint rules define them in the file $SONARQUBE_HOME/extensions/rules/pclint. See Extending rules in C++ analysers for details.
