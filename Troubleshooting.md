This is the list of frequently asked questions and less frequently given answers:

**Q: I don't see any violations after running a SonarQube analysis**

**A:** Possible solutions include: 
* The C++ Community Plugin does not run any static analysis tools itself, make sure that the reports are generated before the analysis (see [[Running tools]]). 
* Be certain the properties are correctly set and the used paths are relative to the project root.
* Be sure that the tools are run in the same location as the analysis. And that you dont move reports between locations with different paths.

**Q: I still dont see any Cppcheck violations in SonarQube**
**A:** Cppcheck supports two different formats for XML reports: 'version 1' and 'version 2'. Make sure you use the former.

