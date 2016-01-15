This is a [SonarQube](http://www.sonarqube.org/) plugin, which adds support for C++ language. It provides following features:

- A full stack of components (preprocessor, lexer and parser) needed to parse, create a model and analyse your sources.
- A parse error recovery, which allows the plugin to skip only those units of code which could not be parsed successfully (experimental).
- A nearly complete support of the standards C++03 and C++11, support for a few GNU and Microsoft extensions.
- Support for the [multi-language feature](http://www.sonarqube.org/at-long-last-sonarqube-is-a-true-polyglot/) found in SonarQube >= 4.2
- Calculation of various size metrics (Number of lines/statements/classes/methods, LOC etc.)
- Feeding of code analysis results for virtually any analyzer, including but not limited to:
  - Cppcheck
  - RATS
  - Vera++
  - Valgrind
- Predefined rules for supported analyzers
- A SQALE Model which covers most of Cppcheck, PC-lint, Vera and Rats rules.
- Cyclomatic (McCabe) complexity metrics
- Code coverage metrics including:
  - Unit test coverage (line and branch)
  - Integration test coverage (line and branch)
  - Overall branch coverage (line and branch)
- Unit test execution metrics
- Recognition of code duplication
- Highlighting mode for C++ in SonarQube UI
- Force include of header files (sonar.cxx.forceIncludes), similar to GCC --include, Visual Studio /FI or cppcheck --include
- Calculation of the public documented API metrics
- Calculation of package cycles and package tangle index

## Dependencies
The plugin doesn't have obligatory dependencies.

However, you may need the following tools in order to extend 
the amount of metrics collected:

- Various external code analyzers:
  - [Cppcheck](http://cppcheck.sourceforge.net/): detects a wide range of problems ranging from performance issues and resource leakage to undefined behaviour. Binary packets are available on/for various platforms. Using the latest release pays off in general; compile from source if in doubt.
  - [RATS](https://code.google.com/p/rough-auditing-tool-for-security/): detects (potential) security problems in code, sensible for code bases with increased security requirements. Use binary packages or compile from source.
  - [Vera++](http://www.inspirel.com/vera/): focuses on code style issues. There's a binary package for Windows, users of other platforms are likely to compile themselves.
  - [Valgrind](http://valgrind.org/): Detects various memory management problems at runtime. Basically Linux only; just use the packages from your distribution.
  - [Pc-Lint](http://www.gimpel.com/html/pcl.htm). Static analyzer from Gimpel Software
- [gcov](http://gcc.gnu.org/onlinedocs/gcc/Gcov.html), [gcovr](http://gcovr.com/), [kcov](https://github.com/SimonKagstrom/kcov) and [Bullseye](http://www.bullseye.com/) for coverage determination.   

## Known Limitations
- Not all of C++ can be parsed by now. You may hit parse errors when analyzing your project.
- The plugin expects to be fed with syntactically correct code. This is a conscious design decision: we do not want to reimplement a compiler and try to follow the KISS principle. Do not expect as much guidance as you can get from a c++ compiler.
- The plugin doesn't know about standard include paths. You have to configure them manually using the property **sonar.cxx.includeDirectories**
- Have also a look at the [issue tracker](https://github.com/wenns/sonar-cxx/issues?state=open)
 