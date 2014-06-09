**Upgrade to 0.9.1**

* Configuration setting ```sonar.cxx.cppncss.reportPath``` is no longer supported.
* Rename configuration setting ```sonar.cxx.externalrules.reportPath``` to ```sonar.cxx.other.reportPath```
* Rename configuration setting ```sonar.cxx.include_directories``` to ```sonar.cxx.includeDirectories```
* Upgrade quality profiles: Search and replace in old quality profile ```<repositoryKey>cxxexternal</repositoryKey>``` with ```<repositoryKey>other</repositoryKey>```. Backup the quality profile as XML and restore it after this replacement again.
* Folder ```..\Sonar\sonar-x.y.z\extensions\rules``` is no longer supported. Add the files to ```sonar.cxx.other.rules``` in the C++ community backend settings instead.
* Lines of Code (LoC) are counted differentially compared to V0.2: Macro definitions are no more counted as LoC. Leads to changes in LoC and derived metrics.