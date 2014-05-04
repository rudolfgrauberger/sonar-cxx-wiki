This is a [SonarQube](http://www.sonarqube.org/) plugin, which adds support for C++ language. It provides following features:

- Calculation of various size metrics (Number of lines/statements/classes/methods, LOC etc.)
- Feeding of code analysis results for virtually any analyzer, including but not limited to:
  - Cppcheck
  - RATS
  - Vera++
  - Valgrind
- Cyclomatic (McCabe) complexity metrics
- Code coverage metrics including:
  - Unit test coverage (line and branch)
  - Integration test coverage (line and branch)
  - Overall branch coverage (line and branch)
- Unit test execution metrics
- Recognition of code duplication
- Highlighting mode for C++ in SonarQube UI

## Dependencies
The plugin doesn't have obligatory dependencies.

However, you may need the following tools in order to extend 
the amount of metrics collected:

- Various external code analyzers:
  - [Cppcheck](http://cppcheck.sourceforge.net/): detects a wide range of problems ranging from performance issues and resource leakage to undefined behaviour. Binary packets are available on/for various platforms. Using the latest release pays off in general; compile from source if in doubt.
  - [RATS](https://www.fortify.com/ssa-elements/threat-intelligence/rats.html): detects (potential) security problems in code, sensible for code bases with increased security requirements. Use binary packages or compile from source.
  - [Vera++](http://www.inspirel.com/vera/): focuses on code style issues. There's a binary package for Windows, users of other platforms are likely to compile themselves.
  - [Valgrind](http://valgrind.org/): Detects various memory management problems at runtime. Basically Linux only; just use the packages from your distribution.
  - [Pc-Lint](http://www.gimpel.com/html/pcl.htm). Static analyzer from Gimpel Software
- [gcov](http://gcc.gnu.org/onlinedocs/gcc/Gcov.html), [gcovr](http://gcovr.com/) and [Bullseye](http://www.bullseye.com/) for coverage determination.   

## Known Limitations
- Not all of C++ can be parsed by now. You may hit parse errors when analyzing your project.
- The the plugin expects to be fed with syntactically correct code. This is a conscious design decision: we do not want to reimplement a compiler and try to follow the KISS principle. Do not expect as much guidance as you can get from a c++ compiler.
- The plugin doesn't know about standard include paths. You have to configure them manually using the property **sonar.cxx.include_directories**
- Have also a look at the [issue tracker](https://github.com/wenns/sonar-cxx/issues?state=open)
 