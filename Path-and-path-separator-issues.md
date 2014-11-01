Setting up the plugin and the build chain the most common issues are path issues at the beginning. Using different build chains, differences on the operating systems and the different SonarQube project types are making the things not easier. On this page you find some hints to get your system up and running.

**General hints**

* The location of your configuration file ```sonar-project.properties``` defines the **root folder** of your project. All other files and folders should be on root level or in a subfolder.<br>*Hint: Only exception is ```sonar.cxx.includeDirectories``` where you can define additional include directories outside of root.*
* Use always slashes (```/```) in the configuration file ```sonar-project.properties``` as path separator. <br>*Hint: It is also possible to use backslashes but you have to escape it with another backslash (```\``` => ```\\```) which is hard to read.*
* Relative paths defined in configuration file are always relative to root folder.
* For all report files use the native path separator of your operating system for path items. This is backslash (\\) on Microsoft Windows and slash (/) on Linux.
* Prefer using absolute paths in report files this makes troubleshooting much easier.<br>*Hint: Relative paths in report files are always relative to root folder (see also Multi-language and Multi-module projects below).*

TBD

**Multi-language projects**

TBD

**Multi-module project**

TBD