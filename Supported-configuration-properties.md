The C++ Community Plugin uses the following properties during analysis. See [here](
http://docs.codehaus.org/display/SONAR/Analyzing+Source+Code) for the ways how to pass them to the plugin.

<table>
<tr>
<td>Property</td>
<td>Scope</td>	
<td>Default</td>
<td>Description</td>
</tr>

<tr>
<td>sonar.cxx.suffixes.sources</td>
<td>system, project</td>
<td>.cxx,.cpp,.cc,.c</td>
<td>Comma separated list of file name extensions to be considered as C++ source files during analysis. 
<br>
Example: .C,.c
</td>
</tr>

<tr>
<td>sonar.cxx.suffixes.headers</td>
<td>system, project</td>
<td>.hxx,.hpp,.hh,.h</td>
<td>Comma separated list of file name extensions to be considered as C++ header files during analysis.
<br>
Example: .H,.h
</td>
</tr>

<tr>
<td>sonar.cxx.includeDirectories</td>
<td>system, project</td>
<td><\td>
<td>Comma separated list of directories where the plugin will be looking for included files.
<br>
Note: the plugin doesn't know any standard include paths. If they should be used, configure them manually using this property.
<br>
Example: include, /usr/include
</td>
</tr>

<tr>
<td>sonar.cxx.forceIncludes</td>
<td>system, project</td>
<td><\td>
<td> Comma separated list of header files to be implicitly included at the beginning of each source file, for details see [[Force Include]]
<br>
Example: VS10Macros.h
</td>
</tr>

<tr>
<td>sonar.cxx.defines<\td>
<td>system, project<\td>
<td><\td>
<td>
List of macros which should be used during analysis. The syntax is the same the body of #define-directives, except the #define keyword itself. This is a multiline property, which means:
<li> If you're using Sonar's Web UI just write a macro per line </li>
<li> When setting via .properties-file seperate macros using '\n\' </li>
<br>
Example for the latter case: 
<code>sonar.cxx.defines = va_arg(a, b) 0, \n\<br>
                          PRIx64 ""       \n\<br>
                          DEBUG 1         
</code>
<\td>
<\tr>

<tr>
<td>sonar.cxx.cppcheck.reportPath</td>
<td>project</td>
<td>cppcheck-reports/cppcheck-result-*.xml</td>
<td>Ant pattern describing the path to Cppcheck reports, <b>relative to projects root</b>.
<br>
Example: cppcheck-report-*.xml
</td>
</tr>

<tr>
<td>sonar.cxx.rats.reportPath</td>
<td>project</td>
<td>rats-reports/rats-result-*.xml</td>
<td>Ant pattern describing the path to RATS reports, <b>relative to projects root</b>.
<br>
Example: rats-report-*.xml
</td>
</tr>

<tr>
<td>sonar.cxx.valgrind.reportPath</td>
<td>project</td>
<td>valgrind-reports/valgrind-result-*.xml</td>
<td>Ant pattern describing the path to Valgrind reports, <b>relative to projects root</b>.
<br>
Example: valgrind-report-*.xml
</td>
</tr>

<tr>
<td>sonar.cxx.vera.reportPath</td>
<td>project</td>
<td>vera++-reports/vera++-result-*.xml</td>
<td>Ant pattern describing the path to Vera++ reports, <b>relative to projects root</b>.
<br>
Example: vera-report-*.xml
</td>
</tr>

<tr>
<td>sonar.cxx.xunit.reportPath</td>
<td>project</td>
<td>xunit-reports/xunit-result-*.xml</td>
<td>Ant pattern describing the path to unit test execution reports, <b>relative to projects root</b>.
<br>
Example: xunit-report-*.xml
</td>
</tr>

<tr>
<td>sonar.cxx.pclint.reportPath</td>
<td>project</td>
<td>pclint-reports/pclint-result-*.xml</td>
<td>Ant pattern describing the path to pc-lint reports, <b>relative to projects root</b>.
<br>
Example: pclint-result-*.xml
</td>
</tr>

<tr>
<td>sonar.cxx.other.reportPath</td>
<td>project</td>
<td>other-result/other-result-*.xml</td>
<td>Ant pattern describing the path to unit test execution reports, <b>relative to projects root</b>.
<br>
Example: other-result-*.xml
</td>
</tr>

<tr>
<td>sonar.cxx.xunit.xsltURL</td>
<td>project</td>
<td></td>
<td>A name of a built in XSLT-file or an URL to an external one. Available builtins:
<li>boosttest-1.x-to-junit-1.0.xsl: For transforming Boost-reports</li>
<li>cpptestunit-1.x-to-junit-1.0.xsl: For transforming CppTestUnit-reports</li>
<li>cppunit-1.x-to-junit-1.0.xsl: For transforming CppUnit-reports</li>
<br>
Example: cppunit-1.x-to-junit-1.0.xsl
</td>
</tr>

<tr>
<td>sonar.cxx.coverage.reportPath</td>
<td>project</td>
<td>coverage-reports/coverage-*.xml</td>
<td>Ant pattern describing the path of unit test coverage reports, <b>relative to projects root</b>.
<br>
Example: coverage-*.xml
</td>
</tr>

<tr>
<td>sonar.cxx.coverage.itReportPath</td>
<td>project</td>
<td>coverage-reports/it-coverage-*.xml</td>
<td>Ant pattern describing the path of integration test coverage reports, <b>relative to projects root</b>.
<br>
Example: it-coverage-*.xml
</td>
</tr>

<tr>
<td>sonar.cxx.coverage.overallReportPath</td>
<td>project</td>
<td>coverage-reports/overall-coverage-*.xml</td>
<td>Ant pattern describing the path of overall test coverage reports, <b>relative to projects root</b>.
<br>
Example: overall-coverage-*.xml
</td>
</tr>

<tr>
<td>sonar.cxx.compiler.reportPath</td>
<td>project</td>
<td>compiler-reports/BuildLog.htm</td>
<td>Ant pattern describing the path to compiler output file, <b>relative to projects root</b>.
The current default settings can be used for VC++ compiler log file.
<br>
Example: BuildLog.htm
</td>
</tr>

<tr>
<td>sonar.cxx.compiler.regex</td>
<td>project</td>
<td>see description</td>
<td>
Regular expression for four groups with this sequence:
<ol>
<li>file name</li>
<li>line number</li>
<li>message id</li>
<li>message text</li>
</ol>
Default: ^.*[\\\\,/](.*)\\(([0-9]+)\\)\\x20:\\x20warning\\x20(C\\d\\d\\d\\d):(.*)$
</td>
<tr>

<tr>
<td>sonar.cxx.compiler.charset</td>
<td>project</td>
<td>UTF-16</td>
<td>
Charset used for the compiler log file (sonar.cxx.compiler.reportPath) e.g. UTF-8, UTF-16 (for more see java.nio.charset.Charset)
<br>
</td>
</tr>
</table>

* Use sonar.cxx.include_directories for the 0.9 release