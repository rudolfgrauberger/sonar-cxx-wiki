
## Description / Features
This is a SonarQube plugin, which adds support for C++ language. It provides following features:

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
- Unit test execution metrics including
- Recognition of code duplication
- Basic highlighting mode for C++ in SonarQube UI

## Installation 
- Download the jar package into the SONARQUBE_HOME/extensions/plugins directory
- Restart the SonarQube server

## Dependencies
The plugin doesn't have obligatory dependencies.

However, you may need the following tools in order to extend 
the amount of metrics collected:

- Various external code analyzers:
  - Cppcheck. Detects a wide range of problems ranging from performance issues and resource leakage to 
    undefined behaviour. Binary packets are available on/for various platforms. Using the latest release   
    pays off in general; compile from source if in doubt.
  - RATS. Detects (potential) security problems in code, sensible for code bases with increased security 
    requirements. Use binary packages or compile from source.
  - Vera++. Focuses on code style issues. There's a binary package for Windows, users of other platforms are 
    likely to compile themselves.
  - Valgrind (memcheck). Detects various memory management problems at runtime. Basically Linux only; just 
    use the packages from your distribution.
  - Pc-Lint. Static analyzer from Gimpel Software
- GCC, gcov, gcovr, Bullseye and Python for coverage determination.   

## Known Limitations
Not all of C++ can be parsed by now. You may hit parse errors when analyzing your project.
The plugin doesnt know about standard include paths. You have to configure them manually using the property **sonar.cxx.include_directories**
 