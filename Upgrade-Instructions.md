**Upgrade to 0.9.6**

* Compatible with SonarQube 5.6.x
* Java Runtime Environment 8 is supported (end of Java 7 support).
* remove deprecated SQALE quality model; `sonar.cxx.other.sqales` is no more supported
* support of new SonarQube quality model; update the [format of the rule files](https://github.com/SonarOpenCommunity/sonar-cxx/wiki/Extending-the-code-analysis#the-format-of-the-rules-file)

**Upgrade to 0.9.5**

* Compatible with SonarQube 4.5.2+, 5.0.x, 5.1.x, 5.3.x, 5.4.x and 5.5.x
* Java Runtime Environment 7 and 8 are supported. JRE 8 is recommended because of higher system performance.
* Undocumented public API detection: documentation for methods marked with "override" is optional now. This results typically in less documentation issues.
* Improved calculation of metric COMPLEXITY_IN_CLASSES. Values for COMPLEXITY_IN_CLASSES can be different.
* TooManyLinesOfCodeInFunctionCheck: improved LOC counting, Values can be different.

**Upgrade to 0.9.4**

* Compatible with SonarQube 4.5.2+, 5.0.x and 5.1.x
* Java Runtime Environment 7 and 8 are supported. JRE 8 is recommended because of higher system performance.
* Default values for ```reportPath``` values has been removed to get meaningful error messages. In case you were using the defaults you have to explicit define them in the ```sonar-project.properties``` file now.
* ```forceZeroCoverage```: Depends on which key (```sonar.cxx.coverage.reportPath```, ```sonar.cxx.coverage.itReportPath```, ```sonar.cxx.coverage.overallReportPath```) is defined in the ```sonar-project.properties``` file now. Defining ```forceZeroCoverage``` alone will no more work.
* It is now possible to define Sqale characteristics for external rules (other) but there are still no predefined values.


**Upgrade to 0.9.3**

* Compatible with SonarQube 4.5.2+, 5.0.x and 5.1.x
* Java Runtime Environment 7 and 8 are supported. JRE 8 is recommended because of higher system performance.
* External rules (other) does not support Sqale characteristics.
* Metric COMMENT_BLANK_LINES is deprecated and no more supported ([SONAR-3768](https://jira.codehaus.org/browse/SONAR-3768)).
* Property ```sonar.cxx.coverage.forceZeroCoverage``` supports line, integration and overall coverage now. 
* Since SonarQube 5.0, there is a built-in support for SCM information on source files. In case you don't want to use it set ```sonar.scm.disabled=true``` to your project configuration to disable [SCM support](http://docs.sonarqube.org/display/SONAR/SCM+support).
* Support of new syntax highlighter API ([SONAR-3893](https://jira.codehaus.org/browse/SONAR-3893)): Formatting of source code is different.
* Cppcheck/inconclusive messages: there is [inconclusive] at the beginning of the message now.
* C++ Community plugin rules visible under 'c++ SonarQube'. Some of the rules has changed rule keys. Especially template rules are not activated by default. Please check listed rules below if they have the same state in your profile as before:
  * FileCyclomaticComplexity => FileComplexity
  * InvalidFileEncoding => FileEncoding
  * UseFileHeader => FileHeader
  * NotAllowedFixMeTag => FixmeTagPresence
  * FunctionCyclomaticComplexity => FunctionComplexity
  * NoHardcodedAccount => HardcodedAccount
  * NoHardcodedIp => HardcodedIp
  * IndentationCheck => Indentation
  * MissingInclude => MissingIncludeFile
  * NewLineAtEOF => MissingNewLineAtEndOfFile
  * ReservedNamesCheck => ReservedNames
  * SafetyTagCheck => SafetyTag
  * SwitchLastCaseIsDefaultCheck => SwitchLastCaseIsDefault
  * NoTabCharacter => TabCharacter
  * NotAllowedToDoTag => TodoTagPresence


**Upgrade to 0.9.2**

* Compatible with SonarQube 4.5
* Coverage: New property ```sonar.cxx.coverage.forceZeroCoverage``` set coverage for source files without coverage report to zero. For V0.9.1 compatibility set value to 'false'.
* Unit Tests: New property ```sonar.cxx.xunit.provideDetails```. To get detailed unit test information set property to 'true'. This is also the V0.9.1 compatibility value. SonarQube does not support 'virtual files' anymore. In case your report files contain 'filename' tags they must match with 'physical files'.


**Upgrade to 0.9.1**

* Compatible with SonarQube 3.7 to 4.2.
* Configuration setting ```sonar.cxx.cppncss.reportPath``` is no longer supported.
* Rename configuration setting ```sonar.cxx.externalrules.reportPath``` to ```sonar.cxx.other.reportPath```
* Rename configuration setting ```sonar.cxx.include_directories``` to ```sonar.cxx.includeDirectories```
* Upgrade quality profiles: Backup the quality profile as XML. Search and replace in old quality profile ```<repositoryKey>cxxexternal</repositoryKey>``` with ```<repositoryKey>other</repositoryKey>```. Restore it after this replacement again.
* Folder ```..\Sonar\sonar-x.y.z\extensions\rules``` is no longer supported. Add file content via settings in the web UI to ```sonar.cxx.other.rules``` in the C++ community backend settings instead.
* Lines of Code (LoC) are counted differentially compared to V0.2: Macro definitions are no more counted as LoC. Leads to changes in LoC and derived metrics.