This is the list of frequently asked questions and less frequently given answers:

**Q: I don't see any violations after running a SonarQube analysis**

**A:** Possible solutions include: 
* The C++ Community Plugin does not run any static analysis tools itself, make sure that the reports are generated before the analysis (see [[Running tools]]). 
* Be certain the properties are correctly set and the used paths are absolute or relative to the project root.
* Be sure that the tools are run in the same location as the analysis. And that you don't move reports between locations with different paths. To ensure that you're not facing a path mismatch issue, run the analysis with debug enabled (using -X parameter) and check the output.

**Q: SonarQube fails to start with error messages: Cannot insert duplicate key row in object 'dbo.rules'**

**A:** This problem can occur when using MS SQL database configured to be case insensitive. Make sure database is set to be case sensitive and restart SonarQube. For more information check database requirements for SonarQube: [Requirements](http://docs.codehaus.org/display/SONAR/Requirements)

**Q: Why does Sonar alternate between two different values for coverage, although the code didn't change inbetween?**

**A:** This effect can be observed if you feed multiple coverage reports which include coverage data for same source files. To prevent this, merge the coverage report outside Sonar before feeding them.