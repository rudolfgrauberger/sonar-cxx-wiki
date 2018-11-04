The Community C++ Plugin supports feeding compiler warnings as violations into SonarQube. Here is a quick guide how to run the supported compilers and catch needed relevant output.

**IMPORTANT**: Quality rules have to be activated in order to enable the import of warnings. Please see [Activate quality rules](https://github.com/SonarOpenCommunity/sonar-cxx/wiki/Activate-quality-rules) for more info.

### GNU C++ Compiler
To feed GCC warnings into SonarQube, make sure to:

1. Add the '-fdiagnostics-show-option' option in your GCC build options (CFLAGS, CPPFLAGS or similar)
2. Capture the warnings from your build into a file (e.g build.log) using shell redirections or similar
3. Set configuration properties, example:
```
sonar.cxx.gcc.reportPath=*.log
sonar.cxx.gcc.charset=UTF-8
```
If gcc outputs the column numbers
```
sonar.cxx.gcc.regex=(?<file>.*):(?<line>[0-9]+):[0-9]+:\\x20warning:\\x20(?<message>.*)\\x20\\[(?<id>.*)\\]
```
Else if gcc doesn't output the column numbers (e.g. -fno-show-column is set or gcc version 4.4.7)
```
sonar.cxx.gcc.regex=(?<file>.*):(?<line>[0-9]+):\\x20warning:\\x20(?<message>.*)\\x20\\[(?<id>.*)\\]
```
Hint: You have to use additional escape sequences (`\`-> `\\`) for the regex property in the configuration file!

4. Activate the rules from the rule repository "compiler-gcc"
5. Run the analysis

### Microsofts Visual Studio Compiler

The compiler sensor consumes the warning messages available in the build log. Depending on the configuration properties there are more or less warnings available. Briefly these are the regular expressions that should be used, see details in next sections.

The format of the build log looks different for parallel project builds (MSBuild options `/maxcpucount:xx`) and the regular expression has to consider this. 

| log type | Example |
|----------|---------|
| single process | `c:\program files (x86)\microsoft visual studio 12.0\vc\include\string.h(55): warning C4995: 'memcpy': name was marked as #pragma deprecated` |
| multiple processes | ` 1>c:\program files (x86)\microsoft visual studio 12.0\vc\include\string.h(55): warning C4995: 'memcpy': name was marked as #pragma deprecated` |

| Visual Studio Version              | Regular Expression           | 
| ---------------------------------- |----------------------------- | 
| Visual Studio 2010-2015                 | `(.*>)?(?<file>.*)\((?<line>\d+)\)\x20:\x20warning\x20(?<id>C\d+):(?<message>.*)` |

Hint: You have to use additional escape sequences (`\`-> `\\`) for the regex property in the configuration file!

```
sonar.cxx.vc.regex=(.*>)?(?<file>.*)\\((?<line>\\d+)\\)\\x20:\\x20warning\\x20(?<id>C\\d+):(?<message>.*)
```

**Visual Studio settings**

* To create the '[C/C++ Build Warnings C4001-C4999](http://msdn.microsoft.com/en-us/library/8x5x43k7.aspx)' you have to activate the following configuration properties. Open the project property page with ```Project\Properties```. Select ```Configuration Properties\C/C++\General``` and set ```Warning Level``` to ```Level3``` or ```Level4```.

* Enable '[Code Analysis for C/C++ Warnings C6001-C28351](http://msdn.microsoft.com/en-us/library/a5b9aa09.aspx)'. This feature is available in Premium or Ultimate editions only. Select ```Configuration Properties\Code Analysis\General```, activate ```Enable Code Analysis on Build```. As default you can use ```Microsoft Native Recommended Rules```.

* Open ```Tools\Options``` and set option for ```Project and Solutions\Build and Run``` to ```MSBuild Project build log verbosity = Detailed```.

![MSVS cpp.user-property-pages](https://cloud.githubusercontent.com/assets/2315215/3085369/b7b3f4d4-e50f-11e3-8e9e-6d1712db1320.PNG)

**Create the LOG file from the command line**

Visual Studio provides two tools to build and analyze a project from the command line. With both tools it is the easiest to redirect stdout to a LOG file.

```
[devenv.exe|msbuild.exe] ... > output.log
```

Additional both tools provide command line options to redirect the output to a file:


* Devenv example doing a solution rebuild and write the warnings to *example.log*.

```
rem VS2010
call "%ProgramFiles(x86)%\Microsoft Visual Studio 10.0\Common7\Tools\vsvars32.bat"
devenv example.sln /rebuild Release /out example.log

```

* MSBuild example doing a project rebuild and write the warnings to *example.log*.
```
rem VS2010
call "%ProgramFiles(x86)%\Microsoft Visual Studio 10.0\Common7\Tools\vsvars32.bat"
MSBuild.exe example.proj /t:rebuild /p:Configuration=Release;WarningLevel=3 /fileLogger /fileLoggerParameters:WarningsOnly;LogFile=example.log;Verbosity=detailed;Encoding=UTF-8

```
**Retrieving compiler information from buildlog**

Version 0.9.3 and above extracts includes, defines and compiler options from the build log automatically (`sonar.cxx.compiler.reportPath`). Starting with version 1.2.0 you have to use `sonar.cxx.msbuild.reportPath`.

This feature is enabled only if the produced log during compilation contains enough information (msbuild verbosity set to detailed or diagnostic). For example
   
```
msbuild.exe /v:Detailed  Solution.SLN > buildlog.log
```

and then

```
sonar.cxx.msbuild.reportPath=buildlog.log
sonar.cxx.msbuild.charset=UTF-8
```

will automate much of the plugin configuration, otherwise set using `sonar.cxx.includeDirectories` and `sonar.cxx.defines`.

This feature can be used in any version of visual studio and  it is independent of the Code Analysis described in earlier sections.

**SonarQube Configuration settings**

To read the messages from the LOG file the following configuration settings have to be defined. The regular expression can be configured and must match to the format in the LOG file.

```
sonar.cxx.vc.reportPath=*.log
sonar.cxx.vc.charset=UTF-8
sonar.cxx.vc.regex=(.*>)?(?<file>.*)\\((?<line>\\d+)\\)\\x20:\\x20warning\\x20(?<id>C\\d+):(?<message>.*)
```

A typical log file contains compiler warnings as shown in the following excerpt:
```
Build started 26.02.2014 17:59:20.
     1>Project "D:\training-kit\plaza_common\Source\sample.dll.vcxproj" on node 3 (Rebuild target(s)).
     1>_PrepareForClean:
         Deleting file "..\..\..\bin\x86\Debug\sample\sample.tlog\pcvcom.lastbuildstate".
       InitializeBuildStatus:
         Creating "..\..\..\bin\x86\Debug\sample\sample.tlog\unsuccessfulbuild" because "AlwaysCreate" was specified.
       ClCompile:
         C:\Program Files (x86)\Microsoft Visual Studio 12.0\VC\bin\CL.exe /c /I..\..\..\boost\include ... (truncated) ...  stdafx.cpp
     1>c:\program files (x86)\microsoft visual studio 12.0\vc\include\string.h(55): warning C4995: 'memcpy': name was marked as #pragma deprecated
     1>c:\program files (x86)\microsoft visual studio 12.0\vc\include\string.h(74): warning C4995: 'memcpy': name was marked as #pragma deprecated
     1>c:\program files (x86)\microsoft visual studio 12.0\vc\include\string.h(112): warning C4995: 'strcpy': name was marked as #pragma deprecated
```

**TFS builds with SonarQube MSBuild scanner**

_Please see some additional hints here [discussion #616](https://github.com/SonarOpenCommunity/sonar-cxx/issues/616)_

### JSON Compilation Database Format Specification support

To support capturing include and define knowledge from other build systems it is possible to utilize [JSON Compilation Database Format Specification](http://clang.llvm.org/docs/JSONCompilationDatabase.html) support. JSON Compilation Database file is used as intermediate format between tools needing information about build process. File contains list of compiled files and how they were compiled.

Sonar C++ plugin supports capturing of compiler defines (`-D`) and include configurations (`-I`) from compiler command lines. These settings are then only affecting analysis of specified file.

In below example `hello.cpp` is compiled with `-DHELLO` and `world.cpp` is compiled with `-DWORLD`:

```
[
  {
    "file" : "hello.cpp"
    "directory": "/home/user/build",
    "command": "/usr/bin/gcc -DHELLO -o hello hello.cpp"
  },
  {
    "file" : "world.cpp"
    "directory": "/home/user/build",
    "command": "/usr/bin/gcc -DWORLD -o world world.cpp"
  }
]
```

This specifies that `HELLO` define is only defined by Sonar C++ plugin when analyzing `hello.cpp` file. Similarly `WORLD` is defined only for `world.cpp`.

To improve define and include knowledge further Sonar C++ plugin includes extension to define includes and defines for all unknown files (like header files) and then allow full definition of both compiler internal and external defines and includes with `defines` and `includes` fields. To define defines and includes for unknown files filename `__global__` is used.

```
[
  {
    "file": "__global__",
    "defines": {
      "__ARM_ARCH": "7",
      "__UINT16_TYPE__": "short unsigned int",
      ...
    },
    "includes" : [
      "/opt/vendor/vendor-sdk/sysroots/x86_64-vendorsdk-linux/usr/lib/arm-vendor-linux-gnueabi/gcc/arm-vendor-linux-gnueabi/4.9.2/include",
      ...
    ]
  },
  {
    "file" : "hello.cpp"
    "directory": "/home/user/build",
    "command": "/usr/bin/gcc -DHELLO -o hello hello.cpp",
    "defines": {
      "__ARM_ARCH": "7",
      "__UINT16_TYPE__": "short unsigned int",
      "__STDC_HOSTED__": "1",
      "__GNUC__" : "4"
      "__SIZEOF_SHORT__": "2",
      "__INT_MAX__": "2147483647",
      ...
      "HELLO" : ""
    },
    "includes" : [
      "/opt/vendor/vendor-sdk/sysroots/x86_64-vendorsdk-linux/usr/lib/arm-vendor-linux-gnueabi/gcc/arm-vendor-linux-gnueabi/4.9.2/include",
      "/opt/vendor/vendor-sdk/sysroots/x86_64-vendorsdk-linux/usr/lib/arm-vendor-linux-gnueabi/gcc/arm-vendor-linux-gnueabi/4.9.2/include-fixed",
      "/opt/vendor/vendor-sdk/sysroots/cortexa8hf-vfp-neon-vendor-linux-gnueabi/usr/include/c++/4.9.2",
      "/opt/vendor/vendor-sdk/sysroots/cortexa8hf-vfp-neon-vendor-linux-gnueabi/usr/include/c++/4.9.2/arm-vendor-linux-gnueabi",
      ...
    ]
  }
]
```

To enable Sonar C++ analysis to utilize JSON compilation database support setting `sonar.cxx.jsonCompilationDatabase` needs to be defined in `sonar-project.properties`.

```
sonar.cxx.jsonCompilationDatabase=compile_commands.json
```

It is also possible to limit scanning of sources only to those specified in JSON compilation database file with setting `sonar.cxx.scanOnlySpecifiedSources`:

```
sonar.cxx.scanOnlySpecifiedSources=True
```
