Changes on the plugin should follow the below design guidelines:

- the main purpose of the plugin is to forward reports from 3rd party tools to SonarQube
  - we don't like to reinvent the wheel
- The plugin expects to be fed with syntactically correct code. This is a conscious design decision: we do not want to reimplement a compiler.
- the plugin is responsible for syntax highlighting
- the plugin is responsible to create software metrics
- we always try to follow the KISS principle

**erroneous configuration:**
- in case of an erroneous configuration the scanner should stop with an error
  - should not create a new snapshot on the SonarQube server
- configuration errors are logged in the LOG file
- configuration errors should not lead to technical debt

**erroneous reports:**
- we support a tolerant and strict error handling mode (sonar.cxx.errorRecoveryEnabled)
   - in tolerant mode (True) analysis continue in case of errors in a report file
   - in strict mode (False) an error in a report file will stop the analysis

**source code parsing:**
- we support a tolerant and strict error handling mode (sonar.cxx.errorRecoveryEnabled)
   - in tolerant mode (True) syntax errors within a declaration are skipped, analysis is continued with next declaration in source code file
   - in strict mode (False) analysis of source code file fails after a syntax error. Source code file is ignored.
