The C++ Community Plugin uses the following properties during analysis. See [here](
http://docs.codehaus.org/display/SONAR/Analyzing+Source+Code) for the ways how to pass them to the plugin.

Beside the general SonarQube [Analysis Parameters](http://docs.codehaus.org/display/SONAR/Analysis+Parameters) the latest released plugin supports the parameter below:

<table>
<tr>
<td>Property</td>
<td>Description</td>
</tr>

<tr>
<td>sonar.cxx.suffixes.sources</td>
<td>Comma separated list of file name extensions to be considered as C++ source files during analysis.
<br>
<i>Scope:</i> system, project
<br>
<i>Default:</i> .cxx,.cpp,.cc,.c
</td>
</tr>

<tr>
<td>sonar.cxx.suffixes.headers</td>
<td>Comma separated list of file name extensions to be considered as C++ header files during analysis.
<br>
<i>Scope:</i> system, project
<br>
<i>Default:</i> .hxx,.hpp,.hh,.h
</td>
</tr>

<tr>
<td>sonar.cxx.includeDirectories</td>
<td>Comma separated list of directories where the plugin will be looking for included files.
<br>
Note: the plugin doesn't know any standard include paths. If they should be used, configure them manually using this property.
<br>
<i>Example:</i> include, /usr/include
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
<i>Example:</i> VS10Macros.h
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
<li> When setting via .properties-file seperate macros using '\n\' </li>
<br>
<i>Example:</i>
<code>sonar.cxx.defines = va_arg(a, b) 0, \n\<br>
                          PRIx64 ""       \n\<br>
                          DEBUG 1
</code>
<br>
<i>Scope:</i> system, project
<br>
<i>Default:</i>
<\td>
<\tr>

<tr>
<td>sonar.cxx.cppcheck.reportPath</td>
<td>Ant pattern describing the path to Cppcheck reports, <b>relative to projects root</b>.
<br>
<i>Scope:</i> project
<br>
<i>Default:</i> cppcheck-reports/cppcheck-result-*.xml
</td>
</tr>

<tr>
<td>sonar.cxx.rats.reportPath</td>
<td>Ant pattern describing the path to RATS reports, <b>relative to projects root</b>.
<br>
<i>Scope:</i> project
<br>
<i>Default:</i> rats-reports/rats-result-*.xml
</td>
</tr>

<tr>
<td>sonar.cxx.valgrind.reportPath</td>
<td>Ant pattern describing the path to Valgrind reports, <b>relative to projects root</b>.
<br>
<i>Scope:</i> project
<br>
<i>Default:</i> valgrind-reports/valgrind-result-*.xml
</td>
</tr>

<tr>
<td>sonar.cxx.vera.reportPath</td>
<td>Ant pattern describing the path to Vera++ reports, <b>relative to projects root</b>.
<br>
<i>Scope:</i> project
<br>
<i>Default:</i> vera++-reports/vera++-result-*.xml
</td>
</tr>

<tr>
<td>sonar.cxx.xunit.reportPath</td>
<td>Ant pattern describing the path to unit test execution reports, <b>relative to projects root</b>.
<br>
<i>Scope:</i> project
<br>
<i>Default:</i> xunit-reports/xunit-result-*.xml
</td>
</tr>

<tr>
<td>sonar.cxx.pclint.reportPath</td>
<td>Ant pattern describing the path to pc-lint reports, <b>relative to projects root</b>.
<br>
<i>Scope:</i> project
<br>
<i>Default:</i> pclint-reports/pclint-result-*.xml
</td>
</tr>

<tr>
<td>sonar.cxx.other.reportPath</td>
<td>Ant pattern describing the path to unit test execution reports, <b>relative to projects root</b>.
<br>
<i>Scope:</i> project
<br>
<i>Default:</i> other-result/other-result-*.xml
</td>
</tr>

<tr>
<td>sonar.cxx.xunit.xsltURL</td>
<td>A name of a built in XSLT-file or an URL to an external one. Available builtins:
<li>boosttest-1.x-to-junit-1.0.xsl: For transforming Boost-reports</li>
<li>cpptestunit-1.x-to-junit-1.0.xsl: For transforming CppTestUnit-reports</li>
<li>cppunit-1.x-to-junit-1.0.xsl: For transforming CppUnit-reports</li>
<br>
<i>Example</i>: cppunit-1.x-to-junit-1.0.xsl
<br>
<i>Scope:</i> project
<br>
<i>Default:</i>
</td>
</tr>

<tr>
<td>sonar.cxx.coverage.reportPath</td>
<td>Ant pattern describing the path of unit test coverage reports, <b>relative to projects root</b>.
<br>
<i>Scope:</i> project
<br>
<i>Default:</i> coverage-reports/coverage-*.xml
</td>
</tr>

<tr>
<td>sonar.cxx.coverage.itReportPath</td>
<td>Ant pattern describing the path of integration test coverage reports, <b>relative to projects root</b>.
<br>
<i>Scope:</i> project
<br>
<i>Default:</i> coverage-reports/it-coverage-*.xml
</td>
</tr>

<tr>
<td>sonar.cxx.coverage.overallReportPath</td>
<td>Ant pattern describing the path of overall test coverage reports, <b>relative to projects root</b>.
<br>
<i>Scope:</i> project
<br>
<i>Default:</i> coverage-reports/overall-coverage-*.xml
</td>
</tr>

<tr>
<td>sonar.cxx.compiler.reportPath</td>
<td>Ant pattern describing the path to compiler output file, <b>relative to projects root</b>.
The current default settings can be used for VC++ compiler log file.
<br>
<i>Scope:</i> project
<br>
<i>Default:</i> compiler-reports/BuildLog.htm
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
<i>Default:</i> ^.*[\\\\,/](.*)\\(([0-9]+)\\)\\x20:\\x20warning\\x20(C\\d\\d\\d\\d):(.*)$
</td>
<tr>

<tr>
<td>sonar.cxx.compiler.charset</td>
<td>
Charset used for the compiler log file (sonar.cxx.compiler.reportPath) e.g. UTF-8, UTF-16 (for more see java.nio.charset.Charset)
<br>
<i>Scope:</i> project
<br>
<i>Default:</i> UTF-16
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
