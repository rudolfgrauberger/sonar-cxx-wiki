The C++ Community Plugin uses the following properties during analysis. See [here](
http://docs.codehaus.org/display/SONAR/Analyzing+Source+Code) for the ways how to pass them to the plugin.

Beside the general SonarQube [Analysis Parameters](http://docs.codehaus.org/display/SONAR/Analysis+Parameters) the latest released plugin supports the parameter below:

* [sonar.cxx.suffixes.sources](https://github.com/SonarOpenCommunity/sonar-cxx/wiki/Supported-configuration-properties#sonarcxxsuffixessources)
* [sonar.cxx.suffixes.headers](https://github.com/SonarOpenCommunity/sonar-cxx/wiki/Supported-configuration-properties#sonarcxxsuffixesheaders)
* [sonar.cxx.includeDirectories](https://github.com/SonarOpenCommunity/sonar-cxx/wiki/Supported-configuration-properties#sonarcxxincludedirectories)
* [sonar.cxx.forceIncludes](https://github.com/SonarOpenCommunity/sonar-cxx/wiki/Supported-configuration-properties#sonarcxxforceincludes)
* [sonar.cxx.defines](https://github.com/SonarOpenCommunity/sonar-cxx/wiki/Supported-configuration-properties#sonarcxxdefines)
* [sonar.cxx.cFilesPatterns](https://github.com/SonarOpenCommunity/sonar-cxx/wiki/Supported-configuration-properties#sonarcxxcfilespatterns)
* [sonar.cxx.errorRecoveryEnabled](https://github.com/SonarOpenCommunity/sonar-cxx/wiki/Supported-configuration-properties#sonarcxxerrorrecoveryenabled)
* [sonar.cxx.cpd.ignoreLiterals](https://github.com/SonarOpenCommunity/sonar-cxx/wiki/Supported-configuration-properties#sonarcxxcpdignoreliterals)
* [sonar.cxx.cpd.ignoreIdentifiers](https://github.com/SonarOpenCommunity/sonar-cxx/wiki/Supported-configuration-properties#sonarcxxcpdignoreidentifiers)
* [sonar.cxx.cppcheck.reportPath](https://github.com/SonarOpenCommunity/sonar-cxx/wiki/Supported-configuration-properties#sonarcxxcppcheckreportpath)
* [sonar.cxx.rats.reportPath](https://github.com/SonarOpenCommunity/sonar-cxx/wiki/Supported-configuration-properties#sonarcxxratsreportpath)
* [sonar.cxx.valgrind.reportPath](https://github.com/SonarOpenCommunity/sonar-cxx/wiki/Supported-configuration-properties#sonarcxxvalgrindreportpath)
* [sonar.cxx.vera.reportPath](https://github.com/SonarOpenCommunity/sonar-cxx/wiki/Supported-configuration-properties#sonarcxxverareportpath)
* [sonar.cxx.drmemory.reportPath](https://github.com/SonarOpenCommunity/sonar-cxx/wiki/Supported-configuration-properties#sonarcxxdrmemoryreportpath)
* [sonar.cxx.xunit.reportPath](https://github.com/SonarOpenCommunity/sonar-cxx/wiki/Supported-configuration-properties#sonarcxxxunitreportpath)
* [sonar.cxx.xunit.xsltURL](https://github.com/SonarOpenCommunity/sonar-cxx/wiki/Supported-configuration-properties#sonarcxxxunitxsltURL)
* [sonar.cxx.xunit.provideDetails](https://github.com/SonarOpenCommunity/sonar-cxx/wiki/Supported-configuration-properties#sonarcxxxunitprovidedetails)
* [sonar.cxx.vstest.reportsPaths](https://github.com/SonarOpenCommunity/sonar-cxx/wiki/Supported-configuration-properties#sonarcxxvstestreportspaths)
* [sonar.cxx.nunit.reportsPaths](https://github.com/SonarOpenCommunity/sonar-cxx/wiki/Supported-configuration-properties#sonarcxxnunitreportspaths)
* [sonar.cxx.xunit.reportsPaths](https://github.com/SonarOpenCommunity/sonar-cxx/wiki/Supported-configuration-properties#sonarcxxxunitreportspaths)
* [sonar.cxx.pclint.reportPath](https://github.com/SonarOpenCommunity/sonar-cxx/wiki/Supported-configuration-properties#sonarcxxpclintreportpath)
* [sonar.cxx.other.reportPath](https://github.com/SonarOpenCommunity/sonar-cxx/wiki/Supported-configuration-properties#sonarcxxotherreportpath)
* [sonar.cxx.other.sqales](https://github.com/SonarOpenCommunity/sonar-cxx/wiki/Supported-configuration-properties#sonarcxxothersqales)
* [sonar.cxx.coverage.reportPath](https://github.com/SonarOpenCommunity/sonar-cxx/wiki/Supported-configuration-properties#sonarcxxcoveragereportpath)
* [sonar.cxx.coverage.itReportPath](https://github.com/SonarOpenCommunity/sonar-cxx/wiki/Supported-configuration-properties#sonarcxxcoverageitreportpath)
* [sonar.cxx.coverage.overallReportPath](https://github.com/SonarOpenCommunity/sonar-cxx/wiki/Supported-configuration-properties#sonarcxxcoverageoverallreportpath)
* [sonar.cxx.coverage.forceZeroCoverage](https://github.com/SonarOpenCommunity/sonar-cxx/wiki/Supported-configuration-properties#sonarcxxcoverageforcezerocoverage)
* [sonar.cxx.compiler.parser](https://github.com/SonarOpenCommunity/sonar-cxx/wiki/Supported-configuration-properties#sonarcxxcompilerparser)
* [sonar.cxx.compiler.reportPath](https://github.com/SonarOpenCommunity/sonar-cxx/wiki/Supported-configuration-properties#sonarcxxcompilerreportpath)
* [sonar.cxx.compiler.regex](https://github.com/SonarOpenCommunity/sonar-cxx/wiki/Supported-configuration-properties#sonarcxxcompilerregex)
* [sonar.cxx.compiler.charset](https://github.com/SonarOpenCommunity/sonar-cxx/wiki/Supported-configuration-properties#sonarcxxcompilercharset)
* [sonar.cxx.jsonCompilationDatabase](https://github.com/SonarOpenCommunity/sonar-cxx/wiki/Supported-configuration-properties#sonarcxxjsoncompilationdatabase)
* [sonar.cxx.scanOnlySpecifiedSources](https://github.com/SonarOpenCommunity/sonar-cxx/wiki/Supported-configuration-properties#sonarcxxscanonlyspecifiedsources)
* [sonar.cxx.clangsa.reportPath](https://github.com/SonarOpenCommunity/sonar-cxx/wiki/Supported-configuration-properties#sonarcxxclangsareportpath)
* [sonar.cxx.funccomplexity.threshold](https://github.com/SonarOpenCommunity/sonar-cxx/wiki/Supported-configuration-properties#sonarcxxfunccomplexitythreshold)
* [sonar.cxx.funcsize.threshold](https://github.com/SonarOpenCommunity/sonar-cxx/wiki/Supported-configuration-properties#sonarcxxfuncsizethreshold)

___
### sonar.cxx.suffixes.sources
*Scope:* `system, project`
<br>
*Default:* `.cxx,.cpp,.cc,.c`

Comma separated list of file name extensions to be considered as C++ source files during analysis.
<br>
<br>
*Example:*

___
### sonar.cxx.suffixes.headers
*Scope:* `system, project`
<br>
*Default:* `.hxx,.hpp,.hh,.h`

Comma separated list of file name extensions to be considered as C++ header files during analysis.
<br>
<br>
*Example:*

___
### sonar.cxx.includeDirectories
*Scope:* `system, project`
<br>
*Default:* `---`

Comma separated list of directories where the plugin will be looking for included files.
* Note: the plugin doesn't know any standard include paths. If they should be used, configure them manually using this property.

<br>
<br>
*Example:* `include, /usr/include`

___
### sonar.cxx.forceIncludes
*Scope:* `system, project`
<br>
*Default:* `---`

Comma separated list of header files to be implicitly included at the beginning of each source file, for details see [[Force Include]]
<br>
<br>
*Example:* `VS10Macros.h`

___
### sonar.cxx.defines
*Scope:* `system, project`
<br>
*Default:* `---`

List of macros which should be used during analysis. The syntax is the same the body of #define-directives, except the #define keyword itself. This is a multiline property, which means:
* If you're using Sonar's Web UI just write a macro per line 
* When setting via .properties-file separate macros using `\n\` 

<br>
*Example:*
<pre>
va_arg(a, b) 0, \n\
PRIx64 ""       \n\
DEBUG 1
</pre>

___
### sonar.cxx.cFilesPatterns
*Scope:* `project`
<br>
*Default:* `*.c,*.C`

Comma-separated list of wildcard patterns used to detect C files. When
a file matches any of the patterns, it is parsed in C-compatibility mode.
<br>
<br>
*Example:*

___
### sonar.cxx.errorRecoveryEnabled
*Scope:* `project, module`
<br>
*Default:* `True`

Defines *tolerant* or *strict* error handling mode. This setting has impact on parsing the source files and reading report files:
* **report files:**
 * error in an report file could be for example invalid file references or line numbers
 * in *tolerant* mode (`True`) analysis continue in case of errors in a report file
 * in *strict* mode (`False`) an error in a report file will stop the analysis
* **source code parsing:**
 * parsing error means that source code file does not fit to C/C++ grammar
 * in *tolerant* mode (`True`) syntax errors within a declaration are skipped, analysis is continued with next declaration in source code file. For details see [Error Recovery](https://github.com/SonarOpenCommunity/sonar-cxx/wiki/Error-Recovery).
 * in *strict* mode (`False`) analysis of source code file fails after an syntax error. Source code file is ignored.

<br>
*Example:* `sonar.cxx.errorRecoveryEnabled=True`


___
### sonar.cxx.cpd.ignoreLiterals
*Scope:* `project, module`
<br>
*Default:* `False`

CPD ignores literal value differences when evaluating a duplicate block. This means that foo=42; and foo=43; will be seen as equivalent.
<br>
<br>
*Example:* `sonar.cxx.cpd.ignoreLiterals=False`

### sonar.cxx.cpd.ignoreIdentifiers
*Scope:* `project, module`
<br>
*Default:* `False`

CPD ignores identifier value differences when evaluating a duplicate block.; i.e., variable names, methods names, and so forth.
<br>
<br>
*Example:* `sonar.cxx.cpd.ignoreIdentifiers=True`

___
### sonar.cxx.cppcheck.reportPath
*Scope:* `project`
<br>
*Default:* `---`

Ant pattern describing the path to Cppcheck reports. Path can be relative or absolute. Single path or comma separated list of paths is supported.
<br>
<br>
*Example:*

___
### sonar.cxx.rats.reportPath
*Scope:* `project`
<br>
*Default:* `---`

Ant pattern describing the path to RATS reports. Path can be relative or absolute. Single path or comma separated list of paths is supported.
<br>
<br>
*Example:*

___
### sonar.cxx.valgrind.reportPath
*Scope:* `project`
<br>
*Default:* `---`

Ant pattern describing the path to Valgrind reports. Path can be relative or absolute. Single path or comma separated list of paths is supported.
<br>
<br>
*Example:*

___
### sonar.cxx.vera.reportPath
*Scope:* `project`
<br>
*Default:* `---`

Ant pattern describing the path to Vera++ reports. Path can be relative or absolute. Single path or comma separated list of paths is supported.
<br>
<br>
*Example:*

___
### sonar.cxx.drmemory.reportPath
*Scope:* `project`
<br>
*Default:* `---`

Ant pattern describing the path to <a href="http://drmemory.org/">Dr Memory</a> reports. Path can be relative or absolute. Single path or comma separated list of paths is supported.
<br>
<br>
*Example:*

___
### sonar.cxx.xunit.reportPath
*Scope:* `project`
<br>
*Default:* `---`

Ant pattern describing the path to unit test execution reports. Path can be relative or absolute. Single path or comma separated list of paths is supported.
<br>
<br>
*Example:*

___
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

___
### sonar.cxx.xunit.provideDetails
*Scope:* `project`
<br>
*Default:* `False`
<br>
*History:* `no more supported with v0.9.7+`

If "True", tries to assign testcases in reports to test resources in SonarQube,
thus making the drilldown to details possible
<br>
<br>
*Example:*

___
### sonar.cxx.vstest.reportsPaths
*Scope:* `project`
<br>
*Default:* `---`

Ant pattern describing the path to unit test execution reports. TRX output from VSTest. Path can be relative or absolute. Single path or comma separated list of paths is supported.
<br>
<br>
*Example:*

___
### sonar.cxx.nunit.reportsPaths
*Scope:* `project`
<br>
*Default:* `---`

Ant pattern describing the path to unit test execution reports. XML output from the NUnit console runner. Path can be relative or absolute. Single path or comma separated list of paths is supported.
<br>
<br>
*Example:*

___
### sonar.cxx.xunit.reportsPaths
*Scope:* `project`
<br>
<br>
*Default:* `---`

Ant pattern describing the path to unit test execution reports (XUnit XML output). Path can be relative or absolute. Single path or comma separated list of paths is supported.
<br>
<br>
*Example:*

___
### sonar.cxx.pclint.reportPath
*Scope:* `project`
<br>
*Default:* `---`

Ant pattern describing the path to PC-lint reports. Path can be relative or absolute. Single path or comma separated list of paths is supported.
<br>
<br>
*Example:*

___
### sonar.cxx.other.reportPath
*Scope:* `project`
<br>
*Default:* `---`

Ant pattern describing the path to other reports. Path can be relative or absolute. Single path or comma separated list of paths is supported.
<br>
<br>
*Example:*

___
### sonar.cxx.other.sqales
*Scope:* `project`
<br>
*Default:* `---`
<br>
*History:* `no more supported with v0.9.6+`

SQALE characteristics for 'external' code analysers. Ant pattern describing the path to SQALE characteristics, <b>relative to projects root</b>.
<br>
<br>
*Example:*

___
### sonar.cxx.coverage.reportPath
*Scope:* `project`
<br>
*Default:* `---`

Ant pattern describing the path of unit test coverage reports. Path can be relative or absolute. Single path or comma separated list of paths is supported.
<br>
<br>
*Example:*

___
### sonar.cxx.coverage.itReportPath
*Scope:* `project`
<br>
*Default:* `---`
<br>
*History:* no more supported with v0.9.9+ (or SQ6.2+)

Ant pattern describing the path of integration test coverage reports. Path can be relative or absolute. Single path or comma separated list of paths is supported.
<br>
<br>
*Example:*

___
### sonar.cxx.coverage.overallReportPath
*Scope:* `project`
<br>
*Default:* `---`
<br>
*History:* no more supported with v0.9.9+ (or SQ6.2+)

Ant pattern describing the path of overall test coverage reports. Path can be relative or absolute. Single path or comma separated list of paths is supported.
<br>
<br>
*Example:*

___
### sonar.cxx.coverage.forceZeroCoverage
*Scope:* `project`
<br>
*Default:* `True`
<br>
*History:* no more supported with v0.9.9+ (or SQ6.2+)

If 'True', source files without coverage report results are set to zero coverage. This results in more realistic overall Technical Debt values. This setting is only enabled if one ore more of the keys sonar.cxx.coverage.reportPath, sonar.cxx.coverage.itReportPath or sonar.cxx.coverage.overallReportPath is defined (e.g. sonar.cxx.coverage.forceZeroCoverage and sonar.cxx.coverage.reportPath for line coverage). In case you have no report you have to assign a dummy report.
<br>
<br>
*Example:*

___
### sonar.cxx.compiler.parser
*Scope:* `project`
<br>
*Default:* `Visual C++`

The format of the warnings file. Currently supported are 'Visual C++' and 'GCC'.
<br>
<br>
*Example:*

___
### sonar.cxx.compiler.reportPath
*Scope:* `project`
<br>
*Default:* `---`

Ant pattern describing the path to compiler output file. Path can be relative or absolute. Single path or comma separated list of paths is supported.
The current default settings can be used for VC++ compiler log file. If available compiler macros and includes will be taken also from build log and used during the pre processing of sources. See [[Compilers]]
<br>
<br>
*Example:*

___
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

___
### sonar.cxx.compiler.charset
*Scope:* `project`
<br>
*Default:* `UTF-16`

Charset used for the compiler log file (sonar.cxx.compiler.reportPath) e.g. UTF-8, UTF-16 (for more see java.nio.charset.Charset)
<br>
<br>
*Example:*

___
### sonar.cxx.jsonCompilationDatabase
*Scope:* `project`
<br>
*Default:* `---`
<br>
*History:* `no more supported with v1.0.0+`

Enable Sonar C++ analysis to utilize JSON compilation database support. Specifies file to be used as JSON compilation database. JSON compilation database is used to improve C++ symbol and include directory knowledge. Sonar C++ plugin also supports extension to allow importing of used compiler's internal symbols and includes.

For more information please see: [JSON compilation database format specification support](https://github.com/SonarOpenCommunity/sonar-cxx/wiki/Compilers#json-compilation-database-format-specification-support)
<br>
<br>
*Example:*

___
### sonar.cxx.scanOnlySpecifiedSources
*Scope:* `project`
<br>
*Default:* `False`

When using JSON compilation database support limit Sonar C++ plugin analysis to specified files in JSON compilation database. This setting can be used to limit analysis to only compiled files.
<br>
<br>
*Example:*

___
### sonar.cxx.clangsa.reportPath
*Scope:* `project`
<br>
*Default:* `---`

Ant pattern describing the path to Clang Static Analyzer plist reports. Path can be relative or absolute. Single path or comma separated list of paths is supported.
<br>
<br>
*Examples:*  
`sonar.cxx.clangsa.reportPath=divzero.plist`  
or  
`sonar.cxx.clangsa.reportPath=analyzer_reports/*/*.plist`

___
### sonar.cxx.funccomplexity.threshold
*Scope:* `project`
<br>
*Default:* `10`

Cyclomatic complexity threshold used to classify a function as complex. The threshold is for the metrics:
- Complex Functions: Number of functions with high cyclomatic complexity
- Complex Functions (%): % of functions with high cyclomatic complexity
- Complex Functions Lines of Code: Number of lines of code in functions with high cyclomatic complexity
- Complex Functions Lines of Code (%): % of lines of code in functions with high cyclomatic complexity
<br>

___
### sonar.cxx.funcsize.threshold
*Scope:* `project`
<br>
*Default:* `20`

Function size threshold to consider a function to be too big. The threshold is for the metrics:
- Big Functions: Number of functions with too many lines
- Big Functions Lines of Code: Number of lines of code in functions with too many lines
- Big Functions (%): Number of lines of code in functions with too many lines
- Big Functions Lines of Code (%): % of lines of code in functions with too many lines
<br>

---

**Hints V1.0.0:**

* Usage of C plugin in parallel.
  * Please keep in mind that the C plugin is still experimental.
  * You can use all cxx configuration properties also for the C plugin: use `sonar.c.xxx` instead of `sonar.cxx.xxx`
  * You have to set specific file extensions in `sonar.cxx.suffixes.sources` and `sonar.c.suffixes.sources`.
  * `sonar.cxx.cFilesPatterns` should be set in the C plugin configuration but not in the Cxx plugin configuration.
* Json compilation database support `sonar.cxx.jsonCompilationDatabase` is also experimental only
  * `sonar.cxx.scanOnlySpecifiedSources` is no more supported. There were conflicts with `sonar.sources` and `sonar.tests`.
* new configuration properties: `sonar.cxx.funccomplexity.threshold` and `sonar.cxx.funcsize.threshold`

**Hints V1.0.0:**

* Usage of C plugin in parallel.
  * Please keep in mind that the C plugin is still experimental.
  * You can use all cxx configuration properties also for the C plugin: use `sonar.c.xxx` instead of `sonar.cxx.xxx`
  * You have to set specific file extensions in `sonar.cxx.suffixes.sources` and `sonar.c.suffixes.sources`.
  * `sonar.cxx.cFilesPatterns` should be set in the C plugin configuration but not in the Cxx plugin configuration.
* Json compilation database support `sonar.cxx.jsonCompilationDatabase` is also experimental only
  * `sonar.cxx.scanOnlySpecifiedSources` is no more supported. There were conflicts with `sonar.sources` and `sonar.tests`.

**Hints V0.9.9:**
* There are some changes in the SQ core API, **starting with SQ 6.2:**
   * The property `sonar.cxx.forceZeroCoverage` is no more supported. There is now a SQ core support basing on `EXECUTABLE_LINES_DATA`.
* `sonar.cxx.coverage.itReportPath` and `sonar.cxx.coverage.overallReportPath` are no more supported by the SQ core. There is no replacement available.
* Usagage of C plugin in parallel.
  * Please keep in mind that the C plugin is still experimental.
  * You can use all cxx configuration properties also for the C plugin: use `sonar.c.xxx` instead of `sonar.cxx.xxx`
  * You have to set specific file extensions in `sonar.cxx.suffixes.sources`.
  * `sonar.cxx.cFilesPatterns` should be set in the C plugin configuration but not in the Cxx plugin configuration.
* Json compilation database support `sonar.cxx.jsonCompilationDatabase` is also experimental only.

**Hints V0.9.8:**
* Clang Static Analyzer support v5.0.0 (plist reports) available: `sonar.cxx.clangsa.reportPath`.
* Clang Tidy support available: `sonar.cxx.clangtidy.reportPath`.
* CxxOtherSensor: XSLT pre-analyse support available:
   * `sonar.cxx.other.N.inputs`,  `sonar.cxx.other.N.outputs`,  `sonar.cxx.other.N.stylesheet` (N=1...9)
* There are some changes in the SQ core API, **starting with SQ 6.2:**
   * The property `sonar.cxx.forceZeroCoverage` is no more supported. There is now a SQ core support basing on `EXECUTABLE_LINES_DATA`.
* `sonar.cxx.coverage.itReportPath` and `sonar.cxx.coverage.overallReportPath` are no more supported by the SQ core. There is no replacement available.
* Usagage of C plugin in parallel.
  * Please keep in mind that the C plugin is still experimental.
  * You can use all cxx configuration properties also for the C plugin: use `sonar.c.xxx` instead of `sonar.cxx.xxx`
  * You have to set specific file extensions in `sonar.cxx.suffixes.sources`.
  * `sonar.cxx.cFilesPatterns` should be set in the C plugin configuration but not in the Cxx plugin configuration.
* Json compilation database support `sonar.cxx.jsonCompilationDatabase` is also experimental only.

**Hints V0.9.7:**
* Improved report handling: there is a tolerant and a strict mode now. In tolerant mode analysis continue in case of errors in a report file. In strict mode an error in a report file will stop the analysis (`sonar.cxx.errorRecoveryEnabled`). In versions before this one behaviour was sometimes strict and sometimes tolerant.
* The default value of `sonar.cxx.errorRecoveryEnabled` is *True* now. To go back to old behaviour set the value to *False*.
* `sonar.cxx.forceZeroCoverage`: better detection of executable lines. Resulting coverage can be slightly different.
* Improved CPD algorithm with additional configuration settings `sonar.cxx.cpd.ignoreLiterals` and `sonar.cxx.cpd.ignoreIdentifiers`. To get same numbers as before set both to `False`.
* `sonar.cxx.xunit.provideDetails`is no more supported

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

