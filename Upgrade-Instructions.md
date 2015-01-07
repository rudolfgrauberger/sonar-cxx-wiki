**Upgrade to 0.9.1**

* Compatible with SonarQube 3.7 to 4.2.
* Configuration setting ```sonar.cxx.cppncss.reportPath``` is no longer supported.
* Rename configuration setting ```sonar.cxx.externalrules.reportPath``` to ```sonar.cxx.other.reportPath```
* Rename configuration setting ```sonar.cxx.include_directories``` to ```sonar.cxx.includeDirectories```
* Upgrade quality profiles: Backup the quality profile as XML. Search and replace in old quality profile ```<repositoryKey>cxxexternal</repositoryKey>``` with ```<repositoryKey>other</repositoryKey>```. Restore it after this replacement again.
* Folder ```..\Sonar\sonar-x.y.z\extensions\rules``` is no longer supported. Add file content via settings in the web UI to ```sonar.cxx.other.rules``` in the C++ community backend settings instead.
* Lines of Code (LoC) are counted differentially compared to V0.2: Macro definitions are no more counted as LoC. Leads to changes in LoC and derived metrics.


**Upgrade to 0.9.2**

* Compatible with SonarQube 4.5
* Coverage: New property ```sonar.cxx.coverage.forceZeroCoverage``` set coverage for source files without coverage report to zero. For V0.9.1 compatibility set value to 'false'.
* Unit Tests: New property ```sonar.cxx.xunit.provideDetails```. To get detailed unit test information set property to 'true'. This is also the V0.9.1 compatibility value. SonarQube does not support 'virtual files' anymore. In case your report files contain 'filename' tags they must match with 'physical files'.
