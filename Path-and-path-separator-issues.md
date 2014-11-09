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

```INI
sonar.sources=src
sonar.tests=tests/unittests
sonar.cxx.cppcheck.reportPath=build/cppcheck-report.xml
```

**General report file hints (simple project, single language)**

* Report files are XML output files from your tools (e.g. XML output from Cppcheck).
* For all report files use the native path separator of your operating system for path items. This is backslash (\\) on Microsoft Windows and slash (/) on Linux.
* Prefer using absolute paths in report files this makes troubleshooting much easier.<br>*Hint: Relative paths in report files are always relative to root folder (see also Multi-language and Multi-module projects below). Start relative paths always with ```.\```on Windows or ```./``` on Linux.*

Cppcheck example on Microsoft Windows with absolute path:
```XML
<?xml version="1.0" encoding="UTF-8"?>
<results>
    <error file="C:\root\src\example.cpp" ... />
</results>
```
Cppcheck example on Microsoft Windows with relative path:
```XML
<?xml version="1.0" encoding="UTF-8"?>
<results>
    <error file=".\src\example.cpp" ... />
</results>
```

**Multi-language Projects (SonarQube 4.2 and later)**

Since SonarQube 4.2, it is possible to run an analysis on a multi-language project. To do so, the ```sonar.language``` property just has to be removed. Conversely, if for some reason you want to perform a single language-only analysis, make sure sonar.language is specified.

SonarQube is using the file extension to define which plugin to use (for this plugin ```sonar.cxx.suffixes.sources```). All other rules are equal to single language projects.

For more hints see [Analyzing with SonarQube Runner](http://docs.codehaus.org/display/SONAR/Analyzing+with+SonarQube+Runner)

**Multi-module Project**

```
Over the last versions there where a lot of changes, especially for multi-module projects.<br>
We recommend to use SonarQube 4.5.1 and Cxx Plugin 0.9.2 or later.
```

A multi-module project consits of different sub-projects (modules) which can be defined by defining
* all the configuration in the properties file in the root folder or
* the configuration in multiple properties files in the root folders of the module subfolders.

Relative paths are handled different for multi-module projects:
* By default, the module base directory is guessed from the module identifier. But it can be redefined using the ```sonar.projectBaseDir``` property.

* If the module is not located directly in the parent folder, but in a deeper directory structure the module base directory can be defined by setting projectBaseDir for each module.
```INI
module1.sonar.projectBaseDir=modules/mod1
module2.sonar.projectBaseDir=modules/mod2
```

* A project that defines modules (or a module that defines sub-modules) cannot define a source code folder to be analyzed.

```
root (folder with sonar-project.properties:1)
|-- module1 (folder with sonar-project.properties:2)
|     |-- src
|-- Module 2 (folder with sonar-project.properties:3)
|     |-- sources
```

sonar-project.properties:1
```INI
# Set modules IDs
sonar.modules=module1,module2
# Modules inherit properties set at parent level
sonar.sources=src
# By default, the base directory for a module is <current_dir>/<module_ID>.
module2.sonar.projectBaseDir=Module 2
```

sonar-project.properties:3
```INI
# Redefine src from base for module2
sonar.sources=sources
```

For more hints see [Analyzing with SonarQube Runner](http://docs.codehaus.org/display/SONAR/Analyzing+with+SonarQube+Runner)

**sonar-runner advanced usage (SonarQube Runner 2.4 and later)**

The root folder of the project to analyze can be set through the sonar.projectBaseDir property since SonarQube Runner 2.4 (was previously project.home). This folder must contain a sonar-project.properties file if the mandatory properties (like sonar.projectKey) are not specified on the command line.

For more hints see [Analyzing with SonarQube Runner](http://docs.codehaus.org/display/SONAR/Analyzing+with+SonarQube+Runner)