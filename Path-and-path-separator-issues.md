```
*** Draft, not reviewed yet ***
```

Setting up the plugin and the build chain the most common issues are path issues at the beginning. Using different build chains, differences on the operating systems and the different SonarQube project types are making the things not easier. On this page you find some hints to get your system up and running.

**General configuration file hints (simple project, single language)**

* The location of your configuration file ```sonar-project.properties``` defines the **root folder** of your project. All other files and folders should be on root level or in a subfolder.<br>*Hint: Only exception is ```sonar.cxx.includeDirectories``` where you can define additional include directories outside of root.*
* Use always slashes (```/```) in the configuration file ```sonar-project.properties``` as path separator. <br>*Hint: It is also possible to use backslashes but you have to escape it with another backslash (```\``` => ```\\```) which is hard to read.*
* Relative paths defined in configuration file are always relative to root folder.

```
root (folder with sonar-project.properties)
|-- src (folder with source files)
|-- tests
|     |-- unittests (folder with unit test results)
|-- build (folder with reports)
```

resulting sonar-project.properties:

```
sonar.sources=src
sonar.tests=tests/unittests
sonar.cxx.cppcheck.reportPath=build/cppcheck-report.xml
```

**General report file hints (simple project, single language)**

* For all report files use the native path separator of your operating system for path items. This is backslash (\\) on Microsoft Windows and slash (/) on Linux.
* Prefer using absolute paths in report files this makes troubleshooting much easier.<br>*Hint: Relative paths in report files are always relative to root folder (see also Multi-language and Multi-module projects below).*

**Multi-language Projects**

Since SonarQube 4.2, it is possible to run an analysis on a multi-language project. To do so, the ```sonar.language``` property just has to be removed. Conversely, if for some reason you want to perform a single language-only analysis, make sure sonar.language is specified.

SonarQube is using the file extension to define which plugin to use (for this plugin ```sonar.cxx.suffixes.sources```). All other rules are equal to single language projects.

For more hints see http://docs.codehaus.org/display/SONAR/Analyzing+with+SonarQube+Runner

**Multi-module Project**

For more hints see http://docs.codehaus.org/display/SONAR/Analyzing+with+SonarQube+Runner

TBD