**Upgrade to 0.9.1**

* Compatible with SonarQube 3.7 to 4.2.
* Configuration setting ```sonar.cxx.cppncss.reportPath``` is no longer supported.
* Rename configuration setting ```sonar.cxx.externalrules.reportPath``` to ```sonar.cxx.other.reportPath```
* Rename configuration setting ```sonar.cxx.include_directories``` to ```sonar.cxx.includeDirectories```
* Upgrade quality profiles: Backup the quality profile as XML. Search and replace in old quality profile ```<repositoryKey>cxxexternal</repositoryKey>``` with ```<repositoryKey>other</repositoryKey>```. Restore it after this replacement again.
* Folder ```..\Sonar\sonar-x.y.z\extensions\rules``` is no longer supported. Add file content via settings in the web ui to ```sonar.cxx.other.rules``` in the C++ community backend settings instead.
* Lines of Code (LoC) are counted differentially compared to V0.2: Macro definitions are no more counted as LoC. Leads to changes in LoC and derived metrics.