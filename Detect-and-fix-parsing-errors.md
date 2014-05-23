To get meaningful results there should be no syntax errors in your code. This page contains a step-by-step instruction how to find and fix these kind of problems.

In case the plugin is not able to read the code this will result in [[Error Recovery]] and you will see the line below in the analyzer output:
```
15:54:45.567 WARN  - [example.cpp:3]: syntax error, skip 'func1'
```
Second message you should watch for is:
```
15:54:46.567 WARN  - [example.cpp:1]: cannot find the sources for '#include <...>'
```
In both cases you should try to remove them with the hints on this page:

**Provide syntactically correct code**

The plugin expects to be fed with syntactically correct code. This is a conscious design decision: we do not want to re-implement a compiler and try to follow the KISS principle. Therefor the first step should be always to verify your code base on your target system with your build environment for correctness. Your build environment will give you more guidance as the C++ community plugin will do. Typical problems during 
this step are:
* libraries from build environment are missing
* not all sources are available, especially 3rd party libraries are often missing
* source code checked out in different folders: includes can't be resolved

**Missing preprocessor definitions**

To parse the code in the same way as in your build environment you have to set the same macros as in your build environment. Copy your project specific macros to [sonar.cxx.defines](https://github.com/wenns/sonar-cxx/wiki/Supported-configuration-properties). For system specific macros it is in most cases easier to write once a header file for the target build environment and reuse this header file with [[Force Include]] in all projects. For more help see:
* [[Predefined Macros]]
* [[Dealing with compiler specific code peaces]]

Visual Studio:
* Project settings: Property Page / Configuration properties / C/C++ / Preprocessor / Preprocessor Definitions
* Visual Studio [Predefined Macros](http://msdn.microsoft.com/en-us/library/b0084kay.aspx)

**Missing include paths**

In most cases you also have to provide include paths. The plugin doesn't know any standard include paths and also no project specific paths. Copy the paths from your build environment and project to [sonar.cxx.includeDirectories](https://github.com/wenns/sonar-cxx/wiki/Supported-configuration-properties).

Visual Studio:
* Property Page / Configuration properties / VC++ Directories / Include Directories
* Property Page / Configuration properties / C/C++ / General / Additional Include Directories

**Missing support of compiler specific extensions**

C++ community plugin implements a C++03 and C++11 compatible grammar but most compilers support additional compiler specific extensions. To get no syntax errors and meaningful results you have to find workarounds for these extensions. To keep the compiler grammer as simple as possible it was a conscious design decision to support such extensions mainly with marco definitions and not by an extension of the grammar. There are only some exceptions to this, where preprocessor directives won't work, see [[Supported compiler specific extensions]]. [[Dealing with compiler specific code peaces]] gives you an introduction how to do this.
* [Microsoft-Specific Modifiers](http://msdn.microsoft.com/en-us/library/6bh0054z.aspx)
* [GNU compiler extensions to the C++ Language](http://gcc.gnu.org/onlinedocs/gcc-4.9.0/gcc/C_002b_002b-Extensions.html)

**Incomplete support of C++ specification**

In case there are still problems check if your code fits to the latest C++ specification. In case the plugin does not support the code you can try to mock it away, but in most cases you can only raise an issue in this forum to ask for an extension of the grammar.
