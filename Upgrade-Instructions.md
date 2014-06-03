**Upgrade to 0.9.1**

* configuration setting ```sonar.cxx.cppncss.reportPath``` is no longer supported
* rename configuration setting ```sonar.cxx.externalrules.reportPath``` to ```sonar.cxx.other.reportPath```
* Search and replace in old quality profile XML files ```<repositoryKey>cxxexternal</repositoryKey>``` with ```<repositoryKey>other</repositoryKey>```. Restore the quality profile after these changes again.
* Folder ```..\Sonar\sonar-x.y.z\extensions\rules``` is no longer supported. Add the files to ```sonar.cxx.other.rules``` in the C++ community backend settings.