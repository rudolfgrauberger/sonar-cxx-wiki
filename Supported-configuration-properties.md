The C++ Community Plugin uses the following properties during analysis. See [here](
http://docs.codehaus.org/display/SONAR/Analyzing+Source+Code) for the ways how to pass them to the plugin.

Beside the general SonarQube [Analysis Parameters](http://docs.codehaus.org/display/SONAR/Analysis+Parameters) the latest released plugin supports the parameter below:

===
### sonar.cxx.suffixes.sources
*Scope:* `system, project`
<br>
*Default:* `.cxx,.cpp,.cc,.c`

Comma separated list of file name extensions to be considered as C++ source files during analysis.
<br>
<br>
*Example:*

===
### sonar.cxx.suffixes.headers
*Scope:* `system, project`
<br>
*Default:* `.hxx,.hpp,.hh,.h`

Comma separated list of file name extensions to be considered as C++ header files during analysis.
<br>
<br>
*Example:*

===
### sonar.cxx.includeDirectories
*Scope:* `system, project`
<br>
*Default:* `---`

Comma separated list of directories where the plugin will be looking for included files.
* Note: the plugin doesn't know any standard include paths. If they should be used, configure them manually using this property.

<br>
<br>
*Example:* `include, /usr/include`

===
### sonar.cxx.forceIncludes
*Scope:* `system, project`
<br>
*Default:* `---`

Comma separated list of header files to be implicitly included at the beginning of each source file, for details see [[Force Include]]
<br>
<br>
*Example:* `VS10Macros.h`

===
### sonar.cxx.defines
*Scope:* `system, project`
<br>
<br>
*Default:* `---`

List of macros which should be used during analysis. The syntax is the same the body of #define-directives, except the #define keyword itself. This is a multiline property, which means:
* If you're using Sonar's Web UI just write a macro per line 
* When setting via .properties-file separate macros using `\n\` 
<br>
<br>
*Example:*
<pre>
va_arg(a, b) 0, \n\
PRIx64 ""       \n\
DEBUG 1
</pre>

===
### sonar.cxx.cFilesPatterns
*Scope:* `project`
<br>
*Default:* `*.c,*.C`

Comma-separated list of wildcard patterns used to detect C files. When
a file matches any of the patterns, it is parsed in C-compatibility mode.
<br>
<br>
*Example:*

===
### sonar.cxx.cppcheck.reportPath
*Scope:* `project`
<br>
*Default:* `---`

Ant pattern describing the path to Cppcheck reports. Path can be relative or absolute. Single path or comma separated list of paths is supported.
<br>
<br>
*Example:*

===
### sonar.cxx.rats.reportPath
*Scope:* `project`
<br>
*Default:* `---`

Ant pattern describing the path to RATS reports. Path can be relative or absolute. Single path or comma separated list of paths is supported.
<br>
<br>
*Example:*

===
### sonar.cxx.valgrind.reportPath
*Scope:* `project`
<br>
*Default:* `---`

Ant pattern describing the path to Valgrind reports. Path can be relative or absolute. Single path or comma separated list of paths is supported.
<br>
<br>
*Example:*

===
### sonar.cxx.vera.reportPath
*Scope:* `project`
<br>
*Default:* `---`

Ant pattern describing the path to Vera++ reports. Path can be relative or absolute. Single path or comma separated list of paths is supported.
<br>
<br>
*Example:*

===
### sonar.cxx.drmemory.reportPath
*Scope:* `project`
<br>
*Default:* `---`

Ant pattern describing the path to <a href="http://drmemory.org/">Dr Memory</a> reports. Path can be relative or absolute. Single path or comma separated list of paths is supported.
<br>
<br>
*Example:*

===
### sonar.cxx.xunit.reportPath
*Scope:* `project`
<br>
*Default:* `---`

Ant pattern describing the path to unit test execution reports. Path can be relative or absolute. Single path or comma separated list of paths is supported.
<br>
<br>
*Example:*

===
### sonar.cxx.xunit.xsltURL
*Scope:* `project`
<br>
*Default:* `---`

A name of a built in XSLT-file or an URL to an external one. Available builtins:
* boosttest-1.x-to-junit-1.0.xsl: For transforming Boost-reports
* boosttest-1.x-to-junit-dummy-1.0.xsl: For transforming Boost-reports, simulating virtual files
* cpptestunit-1.x-to-junit-1.0.xsl: For transforming CppTestUnit-reports
* cppunit-1.x-to-junit-1.0.xsl: For transforming CppUnit-reports
<br>
<br>
*Example*: `cppunit-1.x-to-junit-1.0.xsl`

===
### sonar.cxx.xunit.provideDetails
*Scope:* `project`
<br>
*Default:* `False`

If "True", tries to assign testcases in reports to test resources in SonarQube,
thus making the drilldown to details possible
<br>
<br>
*Example:*

===
### sonar.cxx.vstest.reportsPaths
*Scope:* `project`
<br>
*Default:* `---`

Ant pattern describing the path to unit test execution reports. TRX output from VSTest. Path can be relative or absolute. Single path or comma separated list of paths is supported.
<br>
<br>
*Example:*

===
### sonar.cxx.nunit.reportsPaths
*Scope:* `project`
<br>
*Default:* `---`

Ant pattern describing the path to unit test execution reports. XML output from the NUnit console runner. Path can be relative or absolute. Single path or comma separated list of paths is supported.
<br>
<br>
*Example:*

===
### sonar.cxx.xunit.reportsPaths
*Scope:* `project`
<br>
<br>
*Default:* `---`

Ant pattern describing the path to unit test execution reports (XUnit XML output). Path can be relative or absolute. Single path or comma separated list of paths is supported.
<br>
<br>
*Example:*

===
### sonar.cxx.pclint.reportPath
*Scope:* `project`
<br>
*Default:* `---`

Ant pattern describing the path to PC-lint reports. Path can be relative or absolute. Single path or comma separated list of paths is supported.
<br>
<br>
*Example:*

===
### sonar.cxx.other.reportPath
*Scope:* `project`
<br>
*Default:* `---`

Ant pattern describing the path to other reports. Path can be relative or absolute. Single path or comma separated list of paths is supported.
<br>
<br>
*Example:*

===
### sonar.cxx.other.sqales
*Scope:* `project`
<br>
*Default:* `---`

<b>deprecated with v0.9.6:</b> SQALE characteristics for 'external' code analysers. Ant pattern describing the path to SQALE characteristics, <b>relative to projects root</b>.
<br>
<br>
*Example:*

===
### sonar.cxx.coverage.reportPath
*Scope:* `project`
<br>
*Default:* `---`

Ant pattern describing the path of unit test coverage reports. Path can be relative or absolute. Single path or comma separated list of paths is supported.
<br>
<br>
*Example:*

===
### sonar.cxx.coverage.itReportPath
*Scope:* `project`
<br>
*Default:* `---`

Ant pattern describing the path of integration test coverage reports. Path can be relative or absolute. Single path or comma separated list of paths is supported.
<br>
<br>
*Example:*

===
### sonar.cxx.coverage.overallReportPath
*Scope:* `project`
<br>
*Default:* `---`

Ant pattern describing the path of overall test coverage reports. Path can be relative or absolute. Single path or comma separated list of paths is supported.
<br>
<br>
*Example:*

===
### sonar.cxx.coverage.forceZeroCoverage
*Scope:* `project`
<br>
*Default:* `True`

If 'True', source files without coverage report results are set to zero coverage. This results in more realistic overall Technical Debt values. This setting is only enabled if one ore more of the keys sonar.cxx.coverage.reportPath, sonar.cxx.coverage.itReportPath or sonar.cxx.coverage.overallReportPath is defined (e.g. sonar.cxx.coverage.forceZeroCoverage and sonar.cxx.coverage.reportPath for line coverage). In case you have no report you have to assign a dummy report.
<br>
<br>
*Example:*

===
### sonar.cxx.compiler.parser
*Scope:* `project`
<br>
*Default:* `Visual C++`

The format of the warnings file. Currently supported are 'Visual C++' and 'GCC'.
<br>
<br>
*Example:*

===
### sonar.cxx.compiler.reportPath
*Scope:* `project`
<br>
*Default:* `---`

Ant pattern describing the path to compiler output file. Path can be relative or absolute. Single path or comma separated list of paths is supported.
The current default settings can be used for VC++ compiler log file. If available compiler macros and includes will be taken also from build log and used during the pre processing of sources. See [[Compilers]]
<br>
<br>
*Example:*

===
### sonar.cxx.compiler.regex
*Scope:* `project`
<br>
*Default:* `^.*[\\\\,/](.*)\\(([0-9]+)\\)\\x20:\\x20warning\\x20(C\\d\\d\\d\\d):(.*)$`

Regular expression for four groups with this sequence:
* file name
* line number
* message id
* message text

<br>
<br>
*Example:*

===
### sonar.cxx.compiler.charset
*Scope:* `project`
<br>
*Default:* `UTF-16`

Charset used for the compiler log file (sonar.cxx.compiler.reportPath) e.g. UTF-8, UTF-16 (for more see java.nio.charset.Charset)
<br>
<br>
*Example:*

---

**Hints V0.9.6:**
* SQALE quality model is no more supported: ```sonar.cxx.other.sqales```
* support of new [SonarQube Quality Model](https://github.com/SonarOpenCommunity/sonar-cxx/wiki/Extending-the-code-analysis#the-format-of-the-rules-file)
* support of [Dr Memory](http://drmemory.org/) reports: ```sonar.cxx.drmemory.reportPath```
* ```sonar.cxx.xunit.reportsPaths```: XUnit over sonar-dotnet-tests-library is supported now

**Hints V0.9.5:**
* ```sonar.cxx.vstest.reportsPaths```: TRX output from VSTest is supported now
* ```sonar.cxx.nunit.reportsPaths```: XML output from the NUnit console runner is supported now
* ```reportPath```: path can be relative or absolute now. Paths inside and outside of root folder are supported.
* ```reportPath```: Single path or comma separated list of paths is supported.
* Support of placeholder in configuration file. Format is ${xxx}, supported are environment variables, Java system properties and SonarQube properties.

**Hints V0.9.4:**
* Default values for ```reportPath``` values has been removed to get meaningful error messages. In case you were using the defaults you have to explicit define them in the ```sonar-project.properties``` file now.
* ```forceZeroCoverage```: Depends on which key (```sonar.cxx.coverage.reportPath```, ```sonar.cxx.coverage.itReportPath```, ```sonar.cxx.coverage.overallReportPath```) is defined in the ```sonar-project.properties``` file now. Defining ```forceZeroCoverage``` alone will no more work.
* EXPERIMENTAL: It is now possible to define SQALE characteristics for external rules (other) ```sonar.cxx.other.sqales```.

**Hints V0.9.3:**
* Starting with this version it is possible to automatically retrieve includes, defines and compiler options from a Visual Studio log file. Create the log file with the option ```/v:Diagnostic``` and assign it to ```sonar.cxx.compiler.reportPath```.

**Hints V0.9.2:**
* New property ```sonar.cxx.coverage.forceZeroCoverage``` set coverage for source files without coverage report to 0. For V0.9.1 compatibility set value to 'false'.
* New property ```sonar.cxx.xunit.provideDetails```. To get detailed unit test information set property to 'true'. This is also the V0.9.1 compatibility value. Because SonarQube does not support 'virtual files' any more test resources must be available.
* new property ```sonar.cxx.cFilesPatterns```

**Hints V0.9.1:**
* Configuration setting ```sonar.cxx.cppncss.reportPath``` is no longer supported.
* Rename configuration setting ```sonar.cxx.externalrules.reportPath``` to ```sonar.cxx.other.reportPath```
* Rename configuration setting ```sonar.cxx.include_directories``` to ```sonar.cxx.includeDirectories```
* new property ```sonar.cxx.forceIncludes```

**Hints V0.9.0:**
* Use ```sonar.cxx.include_directories``` instead of ```sonar.cxx.includeDirectories```

