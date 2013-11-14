C++ Community Plugin uses the following properties during analysis. See here for the ways how to pass them to the plugin.


<table>
<tr>
<td>Property</td>
<td>Scope</td>	
<td>Default</td>
<td>Example</td>
<td>Description</td>
</tr>

<tr>
<td>sonar.cxx.suffixes.sources</td>
<td>System, project</td>
<td>.cxx,.cpp,.cc,.c</td>
<td>.C,.h</td>
<td>Comma separated list of file name extensions to be considered as C++ source files during analysis.</td>
</tr>

<tr>
<td>sonar.cxx.suffixes.headers<\td>
<td>System, project<\td>
<td>.hxx,.hpp,.hh,.h<\td>
<td><\td>
<td>Comma separated list of file name extensions to be considered as C++ header files during analysis.<\td>
</tr>

<tr>
<td>sonar.cxx.include_directories<\td>
<td>System, project<\td>
<td><\td>
<td>include, /usr/include<\td>
<td>Comma separated list of directories where the plugin will be look for included files.
Note: the plugin doesn't know any standard include paths. If they should be used, configure them manually using this property.<\td>
</tr>

<tr>
<td>sonar.cxx.defines<\td>
<td>system, project<\td>
<td><\td>
<td>
__attribute__(a), va_arg(a\\\\, b) 0, PRIx64 ""
maven properties example:
<sonar.cxx.defines>Q_OBJECT, Q_PROPERTY(text), EXEC_QTEST(Test_QObject\,c), FUNC(a) #a</sonar.cxx.defines>
<\td>
<td>
Comma separated list of macros which should be used during analysis. The syntax is the same as according #define-directives, except:

* The keyword #define at the beginning has to be skipped
* Commas in the macro body have to be escaped with four (in sonar-project.properties) or one (in pom.xml) 
backslashes.

<\td>
<\tr>

</table>






sonar.cxx.cppcheck.reportPath	Project-wide	cppcheck-reports/cppcheck-result-*.xml	cppcheck-report-*.xml	
Ant pattern describing the path to Cppcheck reports, relative to projects root.
sonar.cxx.rats.reportPath	Project-wide	rats-reports/rats-result-*.xml	rats-report-*.xml	Ant pattern describing the path to RATS reports, relative to projects root.
sonar.cxx.valgrind.reportPath	Project-wide	valgrind-reports/valgrind-result-*.xml	valgrind-report-*.xml	Ant pattern describing the path to Valgrind reports, relative to projects root.
sonar.cxx.vera.reportPath	Project-wide	vera++-reports/vera++-result-*.xml	vera-report-*.xml	Ant pattern describing the path to Vera++ reports, relative to projects root.
sonar.cxx.xunit.reportPath	Project-wide	xunit-reports/xunit-result-*.xml	xunit-report-*.xml	Ant pattern describing the path to unit test execution reports, relative to projects root.
sonar.cxx.pclint.reportPath	Project-wide	pclint-reports/pclint-result-*.xml	pclint-result-*.xml	Ant pattern describing the path to pc-lint reports, relative to projects root.
sonar.cxx.externalrules.reportPath	Project-wide	externalrules-result/externalrules-result-*.xml	externalrules-result-*.xml	Ant pattern describing the path to unit test execution reports, relative to projects root.
sonar.cxx.xunit.xsltURL	Project-wide	 	cppunit-1.x-to-junit-1.0.xsl	
A name of a built in XSLT-file or an URL to an external one. Available builtins:
boosttest-1.x-to-junit-1.0.xsl         For transforming Boost-reports
cpptestunit-1.x-to-junit-1.0.xsl      For transforming CppTestUnit-reports
cppunit-1.x-to-junit-1.0.xsl            For transforming CppUnit-reports
sonar.cxx.coverage.reportPath	Project-wide	coverage-reports/coverage-*.xml	coverage-*.xml	Ant pattern describing the path of unit test coverage reports, relative to projects root.
sonar.cxx.coverage.itReportPath	Project-wide	coverage-reports/it-coverage-*.xml	it-coverage-*.xml	Ant pattern describing the path of integration test coverage reports, relative to projects root.
sonar.cxx.coverage.overallReportPath	Project-wide	coverage-reports/overall-coverage-*.xml	overall-coverage-*.xml	Ant pattern describing the path of overall test coverage reports, relative to projects root.
sonar.cxx.compiler.reportPath
 Project-wide	
compiler-reports/BuildLog.htm
 BuildLog.htm	
Ant pattern describing the path to compiler output file, relative to projects root.
The current default settings can be used for VC++ compiler log file (BuildLog.htm).
 sonar.cxx.compiler.regex
 Project-wide	
^.*[\\\\,/](.*)\\(([0-9]+)\\)\\x20:\\x20warning\\x20(C\\d\\d\\d\\d):(.*)$
^.*[\\\\,/](.*)\\(([0-9]+)\\)\\x20:\\x20warning\\x20(C\\d\\d\\d\\d):(.*)$
 Regular expression for 4 groups with this sequence
file name
line number
message id
message text
 sonar.cxx.compiler.charset
 
 Project-wide	 UTF-16	 UTF-16	
Charset used for the compiler log file (sonar.cxx.compiler.reportPath) e.g. UTF-8, UTF-16 (for more see java.nio.charset.Charset)
