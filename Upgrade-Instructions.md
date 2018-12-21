Follow the general [installation steps](https://github.com/SonarOpenCommunity/sonar-cxx/wiki/Installation). Changes in the different versions are described below:

**Upgrade to 1.2.1**

* Compatible with SonarQube 6.7 LTS, 7.0, 7.1, 7.2, 7.3, 7.4 and 7.5
* Java Runtime Environment 8 is supported (Java 9 is not supported).
* `duplicated_lines_density` values are different with SQ 7.5
* Cognitive Complexity support. There are two known limitations:
   * recursion is not handled
   * cognitive complexity per file is not available (Metrics/Coverage/Cognitive Complexity)
* Usage of C plugin in parallel.
  * Please keep in mind that the C plugin is still experimental.
  * You can use all cxx configuration properties also for the C plugin: use `sonar.c.xxx` instead of `sonar.cxx.xxx`
  * You have to set specific (different) file extensions in `sonar.cxx.suffixes.sources` and `sonar.c.suffixes.sources`.
  * Set `sonar.cxx.cFilesPatterns` in the C plugin configuration only (but not in the Cxx plugin configuration).
* Json compilation database support `sonar.cxx.jsonCompilationDatabase` is also experimental only
  * `sonar.cxx.scanOnlySpecifiedSources` is no more supported. There were conflicts with `sonar.sources` and `sonar.tests`.

**Upgrade to 1.2.0**

* Compatible with SonarQube 6.7 LTS, 7.0, 7.1, 7.2, 7.3 and 7.4
* Java Runtime Environment 8 is supported (Java 9 is not supported).
* Ensure that a rule is enabled if you get no results. In new SQ versions the default profile is read-only. The cxx plugin does not enable all rules per default.
* GCC and MSVC compiler sensor can be used at the same time now
  - **BREAKING CHANGE :** `sonar.cxx.compiler` settings are no more supported!
     - use `sonar.cxx.vc` to read MSVC reports
     - use `sonar.cxx.gcc` to read GCC reports
     - use `sonar.cxx.msbuild` to read includes and defines from MSBuild log file
* Complexity metrics are performed on original source code now
  * In the past we were first preprocessing the code and were calculating the complexity metrics on base of the preprocessed code. This could lead to confusing metric numbers because macro code is counted multiple times and could also be from external libraries. **Generated code (among others macro expansions) doesn't affect the calculation of cognitive / cyclomatic complexity now. This can lead to different but easier to understand metrics.**
* Setting `sonar.cxx.missingIncludeWarnings` is no more available. Turn debug info on to get information.
* Cognitive Complexity support. There are two known limitations:
   * recursion is not handled
   * cognitive complexity per file is not available (Metrics/Coverage/Cognitive Complexity)
* Usage of C plugin in parallel.
  * Please keep in mind that the C plugin is still experimental.
  * You can use all cxx configuration properties also for the C plugin: use `sonar.c.xxx` instead of `sonar.cxx.xxx`
  * You have to set specific (different) file extensions in `sonar.cxx.suffixes.sources` and `sonar.c.suffixes.sources`.
  * Set `sonar.cxx.cFilesPatterns` in the C plugin configuration only (but not in the Cxx plugin configuration).
* Json compilation database support `sonar.cxx.jsonCompilationDatabase` is also experimental only
  * `sonar.cxx.scanOnlySpecifiedSources` is no more supported. There were conflicts with `sonar.sources` and `sonar.tests`.

**Upgrade to 1.1.0**

* Compatible with SonarQube 6.7 LTS, 7.0, 7.1 and 7.2
* Java Runtime Environment 8 is supported (Java 9 is not supported).
* Ensure that a rule is enabled if you get no results. In new SQ versions the default profile is read-only. The cxx plugin does not enable all rules per default.
* Cognitive Complexity support. There are two known limitations:
   * recursion is not handled
   * cognitive complexity per file is not available (Metrics/Coverage/Cognitive Complexity)
* Usage of C plugin in parallel.
  * Please keep in mind that the C plugin is still experimental.
  * You can use all cxx configuration properties also for the C plugin: use `sonar.c.xxx` instead of `sonar.cxx.xxx`
  * You have to set specific file extensions in `sonar.cxx.suffixes.sources` and `sonar.c.suffixes.sources`.
  * `sonar.cxx.cFilesPatterns` should be set in the C plugin configuration but not in the Cxx plugin configuration.
* Json compilation database support `sonar.cxx.jsonCompilationDatabase` is also experimental only
  * `sonar.cxx.scanOnlySpecifiedSources` is no more supported. There were conflicts with `sonar.sources` and `sonar.tests`.

**Upgrade to 1.0.0**

* Compatible with SonarQube 6.7 LTS, 7.0 and 7.1
* Java Runtime Environment 8 is supported (Java 9 is not support).
* Ensure that a rule is enabled if you get no results. In new SQ versions the default profile is read-only. The cxx plugin does not enable all rules per default.
* Cognitive Complexity support. There are two known limitations:
   * recursion is not handled
   * cognitive complexity per file is not available (Metrics/Coverage/Cognitive Complexity)
* Usage of C plugin in parallel.
  * Please keep in mind that the C plugin is still experimental.
  * You can use all cxx configuration properties also for the C plugin: use `sonar.c.xxx` instead of `sonar.cxx.xxx`
  * You have to set specific file extensions in `sonar.cxx.suffixes.sources` and `sonar.c.suffixes.sources`.
  * `sonar.cxx.cFilesPatterns` should be set in the C plugin configuration but not in the Cxx plugin configuration.
* Json compilation database support `sonar.cxx.jsonCompilationDatabase` is also experimental only
  * `sonar.cxx.scanOnlySpecifiedSources` is no more supported. There were conflicts with `sonar.sources` and `sonar.tests`.

**Upgrade to 0.9.9**

* Compatible with SonarQube 6.7 LTS
* Java Runtime Environment 8 is supported (Java 9 is not support).
* Ensure that a rule is enabled if you get no results. In new SQ versions the default profile is read-only. The cxx plugin does not enable all rules per default.
* There are some changes in the SQ core API, **starting with SQ 6.2:**
   * The property `sonar.cxx.forceZeroCoverage` is no more supported. There is now a SQ core support basing on `EXECUTABLE_LINES_DATA`.
   * Calculation of coverage values is slightly different now (coverage is typically a little bit higher).
* `sonar.cxx.coverage.itReportPath` and `sonar.cxx.coverage.overallReportPath` are no more supported by the SQ core. There is no replacement available.
   * Documentation metrics are no more supported by SQ. We added plugin specific metrics for `PUBLIC_API`, `PUBLIC_DOCUMENTED_API_DENSITY`, `PUBLIC_UNDOCUMENTED_API` as replacement. History of SQ values is lost.
   * the following metrics are no more supported: `FILE_COMPLEXITY_DISTRIBUTION`, `COMPLEXITY_IN_FUNCTIONS`, `COMPLEXITY_IN_CLASSES` and `FUNCTION_COMPLEXITY_DISTRIBUTION`
* Cognitive Complexity support. There are two known limitations:
   * recursion is not handled
   * cognitive complexity per file is not available (Metrics/Coverage/Cognitive Complexity)
* Usage of C plugin in parallel.
  * Please keep in mind that the C plugin is still experimental.
  * You can use all cxx configuration properties also for the C plugin: use `sonar.c.xxx` instead of `sonar.cxx.xxx`
  * You have to set specific file extensions in `sonar.cxx.suffixes.sources` and `sonar.c.suffixes.sources`.
  * `sonar.cxx.cFilesPatterns` should be set in the C plugin configuration but not in the Cxx plugin configuration.
* Json compilation database support `sonar.cxx.jsonCompilationDatabase` is also experimental only

**Upgrade to 0.9.8**

* Compatible with SonarQube 5.6 LTS, 6.0, 6.1, 6.2, 6.3, 6.4, 6.5, 6.6, 6.7 LTS
* Java Runtime Environment 8 is supported (Java 9 is not support).
* Ensure that a rule is enabled if you get no results. In new SQ versions the default profile is read-only. The cxx plugin does not enable all rules per default.
* There are some changes in the SQ core API, **starting with SQ 6.2:**
   * The property `sonar.cxx.forceZeroCoverage` is no more supported. There is now a SQ core support basing on `EXECUTABLE_LINES_DATA`.
   * Calculation of coverage values is slightly different now (coverage is typically a little bit higher).
   * `sonar.cxx.coverage.itReportPath` and `sonar.cxx.coverage.overallReportPath` are no more supported by the SQ core. There is no replacement available.
   * Documentation metrics are no more supported by SQ. We added plugin specific metrics for `PUBLIC_API`, `PUBLIC_DOCUMENTED_API_DENSITY`, `PUBLIC_UNDOCUMENTED_API` as replacement. History of SQ values is lost.
* Cognitive Complexity support. There are two known limitations:
   * recursion is not handled
   * cognitive complexity per file is not available (Metrics/Coverage/Cognitive Complexity)
* Usage of C plugin in parallel.
  * Please keep in mind that the C plugin is still experimental.
  * You can use all cxx configuration properties also for the C plugin: use `sonar.c.xxx` instead of `sonar.cxx.xxx`
  * You have to set specific file extensions in `sonar.cxx.suffixes.sources` and `sonar.c.suffixes.sources`.
  * `sonar.cxx.cFilesPatterns` should be set in the C plugin configuration but not in the Cxx plugin configuration.
* Json compilation database support `sonar.cxx.jsonCompilationDatabase` is also experimental only

**Upgrade to 0.9.7**

* Compatible with SonarQube 5.6.x, 6.0, 6.1 and 6.2
* Java Runtime Environment 8 is supported (Java 9 is not support).
* Improved report handling: there is a tolerant and a strict mode now. In tolerant mode analysis continue in case of errors in a report file. In strict mode an error in a report file will stop the analysis (`sonar.cxx.errorRecoveryEnabled`). In versions before this one behaviour was sometimes strict and sometimes tolerant.
* The default value of `sonar.cxx.errorRecoveryEnabled` is *True* now. To go back to old behaviour set the value to *False*.
* `sonar.cxx.forceZeroCoverage`: better detection of executable lines. Resulting coverage can be slightly different.
* Improved CPD algorithm with additional configuration settings `sonar.cxx.cpd.ignoreLiterals` and `sonar.cxx.cpd.ignoreIdentifiers`. To get same numbers as before set both to `False`.
* Detailed mode from test metrics is no more supported with SQ 5.6 API (`sonar.cxx.xunit.provideDetails`).
* Computation of package/file tangle metrics no more supported with SQ 5.6 API.
* `Unit Test Success (%)` is no more supported with SQ 5.6 API.
* With SQ 6.2 overall and integration coverage metrics are no more supported.
* remove deprecated SQALE quality model; `sonar.cxx.other.sqales` is no more supported
* support of new SonarQube quality model; update the [format of the rule files](https://github.com/SonarOpenCommunity/sonar-cxx/wiki/Extending-the-code-analysis#the-format-of-the-rules-file)

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