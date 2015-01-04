The C++ Community Plugin uses the following properties during analysis. See [here](
http://docs.codehaus.org/display/SONAR/Analyzing+Source+Code) for the ways how to pass them to the plugin.

Beside the general SonarQube [Analysis Parameters](http://docs.codehaus.org/display/SONAR/Analysis+Parameters) the latest released plugin supports the parameter below:

<table>
<tr>
<td>Property</td>
<td>Description</td>
</tr>

<tr>
<td><smaller>sonar.cxx.suffixes.sources</smaller></td>
<td>Comma separated list of file name extensions to be considered as C++ source files during analysis.
<br>
<i>Scope:</i> system, project
<br>
<i>Default:</i> <code>.cxx,.cpp,.cc,.c</code>
</td>
</tr>

<tr>
<td>sonar.cxx.suffixes.headers</td>
<td>Comma separated list of file name extensions to be considered as C++ header files during analysis.
<br>
<i>Scope:</i> system, project
<br>
<i>Default:</i> <code>.hxx,.hpp,.hh,.h</code>
</td>
</tr>

<tr>
<td>sonar.cxx.includeDirectories</td>
<td>Comma separated list of directories where the plugin will be looking for included files.
<br>
Note: the plugin doesn't know any standard include paths. If they should be used, configure them manually using this property.
<br>
<i>Example:</i> <code>include, /usr/include</code>
<br>
<i>Scope:</i> system, project
<br>
<i>Default:</i>
</td>
</tr>

<tr>
<td>sonar.cxx.forceIncludes</td>
<td> Comma separated list of header files to be implicitly included at the beginning of each source file, for details see [[Force Include]]
<br>
<i>Example:</i> <code>VS10Macros.h</code>
<br>
<i>Scope:</i> system, project
<br>
<i>Default:</i>
</td>
</tr>

<tr>
<td>sonar.cxx.defines<\td>
<td>
List of macros which should be used during analysis. The syntax is the same the body of #define-directives, except the #define keyword itself. This is a multiline property, which means:
<li> If you're using Sonar's Web UI just write a macro per line </li>
<li> When setting via .properties-file separate macros using '\n\' </li>
<br>
<i>Example:</i>
<pre>
va_arg(a, b) 0, \n\
PRIx64 ""       \n\
DEBUG 1
</pre>
<i>Scope:</i> system, project
<br>
<i>Default:</i>
<\td>
<\tr>

<tr>
<td>sonar.cxx.cFilesPatterns</td>
<td>
Comma-separated list of wildcard patterns used to detect C files. When
a file matches any of the patterns, it is parsed in C-compatibility mode.
<br>
<i>Scope:</i> project
<br>
<i>Default:</i> <code>*.c,*.C</code>
</td>
</tr>

<tr>
<td>sonar.cxx.cppcheck.reportPath</td>
<td>Ant pattern describing the path to Cppcheck reports, <b>relative to projects root</b>.
<br>
<i>Scope:</i> project
<br>
<i>Default:</i> <code>cppcheck-reports/cppcheck-result-*.xml</code>
</td>
</tr>

<tr>
<td>sonar.cxx.rats.reportPath</td>
<td>Ant pattern describing the path to RATS reports, <b>relative to projects root</b>.
<br>
<i>Scope:</i> project
<br>
<i>Default:</i> <code>rats-reports/rats-result-*.xml</code>
</td>
</tr>

<tr>
<td>sonar.cxx.valgrind.reportPath</td>
<td>Ant pattern describing the path to Valgrind reports, <b>relative to projects root</b>.
<br>
<i>Scope:</i> project
<br>
<i>Default:</i> <code>valgrind-reports/valgrind-result-*.xml</code>
</td>
</tr>

<tr>
<td>sonar.cxx.vera.reportPath</td>
<td>Ant pattern describing the path to Vera++ reports, <b>relative to projects root</b>.
<br>
<i>Scope:</i> project
<br>
<i>Default:</i> <code>vera++-reports/vera++-result-*.xml</code>
</td>
</tr>

<tr>
<td>sonar.cxx.xunit.reportPath</td>
<td>Ant pattern describing the path to unit test execution reports, <b>relative to projects root</b>.
<br>
<i>Scope:</i> project
<br>
<i>Default:</i> <code>xunit-reports/xunit-result-*.xml</code>
</td>
</tr>

<tr>
<td>sonar.cxx.pclint.reportPath</td>
<td>Ant pattern describing the path to PC-lint reports, <b>relative to projects root</b>.
<br>
<i>Scope:</i> project
<br>
<i>Default:</i> <code>pclint-reports/pclint-result-*.xml</code>
</td>
</tr>

<tr>
<td>sonar.cxx.other.reportPath</td>
<td>Ant pattern describing the path to unit test execution reports, <b>relative to projects root</b>.
<br>
<i>Scope:</i> project
<br>
<i>Default:</i> <code>other-result/other-result-*.xml</code>
</td>
</tr>

<tr>
<td>sonar.cxx.xunit.xsltURL</td>
<td>A name of a built in XSLT-file or an URL to an external one. Available builtins:
<li>boosttest-1.x-to-junit-1.0.xsl: For transforming Boost-reports</li>
<li>cpptestunit-1.x-to-junit-1.0.xsl: For transforming CppTestUnit-reports</li>
<li>cppunit-1.x-to-junit-1.0.xsl: For transforming CppUnit-reports</li>
<br>
<i>Example</i>: <code>cppunit-1.x-to-junit-1.0.xsl</code>
<br>
<i>Scope:</i> project
<br>
<i>Default:</i>
</td>
</tr>

<tr>
<td>sonar.cxx.xunit.provideDetails</td>
<td>
If "True", tries to assign testcases in reports to test resources in SonarQube,
thus making the drilldown to details possible
<br>
<i>Scope:</i> project
<br>
<i>Default:</i> <code>True</code>
</td>
</tr>

<tr>
<td>sonar.cxx.coverage.reportPath</td>
<td>Ant pattern describing the path of unit test coverage reports, <b>relative to projects root</b>.
<br>
<i>Scope:</i> project
<br>
<i>Default:</i> <code>coverage-reports/coverage-*.xml</code>
</td>
</tr>

<tr>
<td>sonar.cxx.coverage.itReportPath</td>
<td>Ant pattern describing the path of integration test coverage reports, <b>relative to projects root</b>.
<br>
<i>Scope:</i> project
<br>
<i>Default:</i> <code>coverage-reports/it-coverage-*.xml</code>
</td>
</tr>

<tr>
<td>sonar.cxx.coverage.overallReportPath</td>
<td>Ant pattern describing the path of overall test coverage reports, <b>relative to projects root</b>.
<br>
<i>Scope:</i> project
<br>
<i>Default:</i> <code>coverage-reports/overall-coverage-*.xml</code>
</td>
</tr>

<tr>
<td>sonar.cxx.coverage.forceZeroCoverage</td>
<td>
If 'True', assign zero line coverage to source files without coverage report(s),
which results in a more realistic overall Technical Debt value.
<br>
<i>Scope:</i> project
<br>
<i>Default:</i> <code>True</code>
</td>
</tr>

<tr>
<td>sonar.cxx.compiler.parser</td>
<td>The format of the warnings file. Currently supported are 'Visual C++' and 'GCC'.
<br>
<i>Scope:</i> project
<br>
<i>Default:</i> <code>Visual C++</code>
</td>
</tr>

<tr>
<td>sonar.cxx.compiler.reportPath</td>
<td>Ant pattern describing the path to compiler output file, <b>relative to projects root</b>.
The current default settings can be used for VC++ compiler log file.
<br>
<i>Scope:</i> project
<br>
<i>Default:</i> <code>compiler-reports/BuildLog.htm</code>
</td>
</tr>

<tr>
<td>sonar.cxx.compiler.regex</td>
<td>
Regular expression for four groups with this sequence:
<ol>
<li>file name</li>
<li>line number</li>
<li>message id</li>
<li>message text</li>
</ol>
<i>Scope:</i> project
<br>
<i>Default:</i> <code>^.*[\\\\,/](.*)\\(([0-9]+)\\)\\x20:\\x20warning\\x20(C\\d\\d\\d\\d):(.*)$</code>
</td>
<tr>

<tr>
<td>sonar.cxx.compiler.charset</td>
<td>
Charset used for the compiler log file (sonar.cxx.compiler.reportPath) e.g. UTF-8, UTF-16 (for more see java.nio.charset.Charset)
<br>
<i>Scope:</i> project
<br>
<i>Default:</i> <code>UTF-16</code>
<br>
</td>
</tr>
</table>

**Hints V0.9.0:**
* Use ```sonar.cxx.include_directories``` instead of ```sonar.cxx.includeDirectories```

**Hints V0.9.1:**
* Configuration setting ```sonar.cxx.cppncss.reportPath``` is no longer supported.
* Rename configuration setting ```sonar.cxx.externalrules.reportPath``` to ```sonar.cxx.other.reportPath```
* Rename configuration setting ```sonar.cxx.include_directories``` to ```sonar.cxx.includeDirectories```
* new properties ```sonar.cxx.forceIncludes```

**Hints V0.9.2:**
* New property ```sonar.cxx.coverage.forceZeroCoverage``` set coverage for source files without coverage report to 0. For V0.9.1 compatibility set value to 'false'.
* New property ```sonar.cxx.xunit.provideDetails```. To get detailed unit test information set property to 'true'. Because SonarQube does not support 'virtual files' any more test resources must be available.
* new property ```sonar.cxx.cFilesPatterns```



