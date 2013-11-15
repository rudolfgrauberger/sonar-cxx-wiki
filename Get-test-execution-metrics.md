To collect test execution metrics with the C++ Community plugin follow the steps below:

1. Get an execution report out of your favorite test framework. See [[Test runners]] for examples.
2. Configure your SonarQube project by setting the property **sonar.cxx.xunit.reportPath** to point to the created report[s] and rerun the analysis.

By default, the JUnitReport format is expected. To import a report in an other format _X_, set the property **sonar.cxx.xunit.xsltURL** to a XSLT stylesheet which is able to perform X -> JUnitReport conversion. A couple of ready-made stylesheets are available [here](https://github.com/wenns/sonar-cxx/tree/master/sonar-cxx-plugin/src/main/resources/xsl):

* boosttest-1.x-to-junit-1.0.xsl:       For transforming Boost-reports
* cpptestunit-1.x-to-junit-1.0.xsl:     For transforming CppTestUnit-reports
* cppunit-1.x-to-junit-1.0.xsl:         For transforming CppUnit-reports