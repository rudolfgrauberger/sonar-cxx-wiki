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

A multi-module project consits of different sub-projects (modules) which can be defined by defining
* all the configuration in the properties file in the root folder or
* the configuration in multiple properties files.

Relative paths are handled different for multi-module projects:
* By default, the module base directory is guessed from the module identifier. But it can be redefined using the ```sonar.projectBaseDir``` property.

* If the module is not located directly in the parent folder, but in a deeper directory structure the module base directory can be defined by setting projectBaseDir for each module.
```
module1.sonar.projectBaseDir=modules/mod1
module2.sonar.projectBaseDir=modules/mod2
```

* A project that defines modules (or a module that defines sub-modules) cannot define a source code folder to be analyzed.

For more hints see http://docs.codehaus.org/display/SONAR/Analyzing+with+SonarQube+Runner

**sonar-runner advanced usage**

The root folder of the project to analyze can be set through the sonar.projectBaseDir property since SonarQube Runner 2.4 (was previously project.home). This folder must contain a sonar-project.properties file if the mandatory properties (like sonar.projectKey) are not specified on the command line.

For more hints see http://docs.codehaus.org/display/SONAR/Analyzing+with+SonarQube+Runner
