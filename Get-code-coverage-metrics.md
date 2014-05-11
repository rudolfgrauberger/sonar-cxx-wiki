### It is not all the same

Talking about coverage the most important question is: what coverage your are talking about. There are different kinds of coverage measurement and each tool has a slightly different way doing it and displaying the results. If you are looking for a very good introduction read [Code Coverage Analysis](http://www.bullseye.com/coverage.html) on the [Bullseye](http://www.bullseye.com) page.

SonarQube API provides the possibility to set the covered lines (setHits) and covered conditions (setConditions). All other metrics are derived from these settings:

* __Line coverage__: On a given line of code, Line coverage simply answers the following question: Has this line of code been executed during the execution of the unit tests?
* __Conditions by line / Covered conditions by line__: These are the number of conditions by line and number of covered conditions by line.
* __Branch coverage__: On each line of code containing some boolean expressions, the branch coverage simply answers the following question: 'Has each boolean expression been evaluated both to true and false?'. This is the density of possible branches in flow control structures that have been followed during unit tests execution.
* __Coverage__: It is a mix of Line coverage and Branch coverage. Its goal is to provide an even more accurate answer to the following question: How much of the source code has been covered by the unit tests?

For more details and exact calculation see [Metric Definitions](http://docs.codehaus.org/plugins/servlet/mobile#Metricdefinitions-Tests) on the SonarQube page.

### Setup the C++ Community Plugin

To collect C++ test coverage metrics with C++ Community Plugin, you have to:

1. Create a coverage report (or many of them) using your favorite coverage tracer (see [[Coverage tracers]] for examples)
2. Configure your project to point to the report and rerun the analysis

Three types of test coverage are supported:  _Unit_, _Integration_ and _Overall_ coverage. Use one of the following configuration properties dependent of the coverage type (see also [[Supported configuration properties]] for details):

* **sonar.cxx.coverage.reportPath** for unit test coverage
* **sonar.cxx.coverage.itReportPath** for integration test coverage
* **sonar.cxx.coverage.overallReportPath** for overall test coverage

The C++ Community plugin accepts two different formats for the test coverage reports, which will be recognized automatically:

* Cobertura XML: the format introduced by [Cobertura](http://cobertura.github.io/cobertura/)
* The XML format used by [Bullseye](http://www.bullseye.com/)

TODO @guwirth: ms code coverage additions

### Notes for BullseyeCoverage users:
SonarQube <3.2 provides metrics for line coverage and branch coverage. Bullseye users have function and branch/decision coverage instead. The C++ Community plugin converts the second directly into branch coverage however line coverage is far more complex and cannot be correlated directly into function coverage.

Line coverage imported from a bullseye report means than function coverage + line branch coverage (this second occurs since SonarQube will not display branch coverage if there isn't a line it associated with it). This means also that overall coverage will be affected in SonarQube and cannot be compared directly to bullseye results. The following pictures illustrates this for a small example project.

![Coverage visualisation for Bullseye users](images/CovBrowser.png)