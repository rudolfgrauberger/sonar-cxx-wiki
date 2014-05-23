TBD guwirth

To get meaningful results there should be no syntax errors in your code. This page contains a step-by-step instruction how to find and fix these kind of problems.

**Provide syntactically correct code**

The plugin expects to be fed with syntactically correct code. This is a conscious design decision: we do not want to re-implement a compiler and try to follow the KISS principle. Therefor the first step should be always to verify your code base on your target system with you build environment for correctness. Your build environment will give you more guidance as the C++ community plugin will do. Typical problems during 
this step are:
* libraries from build environment are missing
* not all sources are available, especially 3rd party libraries are often missing
* source code checked out in different folders: includes can't be resolved

**Missing preprocessor definitions**

To parse the code in the same way as in your build environment you have to set the same macros as in your build environment. Copy your project specific macros to [sonar.cxx.defines](https://github.com/wenns/sonar-cxx/wiki/Supported-configuration-properties). For system specific macros it is in most cases easier to write once a header file for the target build environment and reuse this header file with [[Force Include]] in all projects. For more help see:
* [[Predefined Macros]]
* [[Dealing with compiler specific code peaces]]

**Missing include paths**

**Missing support of compiler specific extensions**

**Incomplete support of C++ specification**

