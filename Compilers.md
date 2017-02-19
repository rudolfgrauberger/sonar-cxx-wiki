The Community C++ Plugin supports feeding compiler warnings as violations into SonarQube. Here is a quick guide how to run the supported compilers and catch needed relevant output.

### GNU C++ Compiler
To feed GCC warnings into SonarQube, make sure to:

1. Add the '-fdiagnostics-show-option' option in your GCC build options (CFLAGS, CPPFLAGS or similar)
2. Capture the warnings from your build into a file (e.g build.log) using shell redirections or similar
3. Set configuration properties, example:
```
sonar.cxx.compiler.parser=GCC
sonar.cxx.compiler.reportPath=*.log
sonar.cxx.compiler.charset=UTF-8
```
If gcc outputs the column numbers
```
sonar.cxx.compiler.regex=^(.*):([0-9]+):[0-9]+: warning: (.*)\\[(.*)\\]$
```
Else if gcc doesn't output the column numbers (e.g. -fno-show-column is set or gcc version 4.4.7)

```
sonar.cxx.compiler.regex=^(.*):([0-9]+): warning: (.*)\\[(.*)\\]$
```
3. Activate the rules from the rule repository "compiler-gcc"
4. Run the analysis

### Microsofts Visual Studio Compiler

The compiler sensor consumes the warning messages available in the build log. Depending on the configuration properties there are more or less warnings available. Briefly these are the regular expressions that should be used, see details in next sections.

The format of the build log looks different for parallel project builds (MSBuild options `/maxcpucount:xx`) and the regular expression has to consider this. 

| log type | Example |
|----------|---------|
| single process | `c:\program files (x86)\microsoft visual studio 12.0\vc\include\string.h(55): warning C4995: 'memcpy': name was marked as #pragma deprecated` |
| multiple processes | ` 1>c:\program files (x86)\microsoft visual studio 12.0\vc\include\string.h(55): warning C4995: 'memcpy': name was marked as #pragma deprecated` |

| Visual Studio Version              | Regular Expression           | 
| ---------------------------------- |----------------------------- | 
| Visual Studio 2010-2015                 | `^(.*)\((\d+)\)\x20*:\x20warning\x20(C\d+):(.*)$` |
| Visual Studio 2010-2015 (`/maxcpucount:xx`)                | `^.*>(.*)\((\d+)\)\x20*:\x20warning\x20(C\d+):(.*)$` |

You have to use additonal escape sequences (`\`-> `\\`) for property or xml files.

```
sonar.cxx.compiler.regex=^.*>(.*)\\((\\d+)\\)\\x20*:\\x20warning\\x20(C\\d+):(.*)$
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

Version 0.9.3 and above extracts includes, defines and compiler options from the build log automatically.

This feature is enabled only if the produced log during compilation contains enough information (msbuild verbosity set to detailed or diagnostic). For example
   
```
msbuild.exe /v:Detailed  Solution.SLN > buildlog.log
```

and then

```
sonar.cxx.compiler.reportPath=buildlog.log
```

will automate much of the plugin configuration, otherwise set using sonar.cxx.includeDirectories and sonar.cxx.defines.

This feature can be used in any version of visual studio and  it is independent of the Code Analysis described in earlier sections. Altough they come together using the same sonar.cxx.compiler.reportPath option.

**SonarQube Configuration settings**

To read the messages from the LOG file the following configuration settings have to be defined. The regular expression can be configured and must match to the format in the LOG file.

```
sonar.cxx.compiler.parser=Visual C++
sonar.cxx.compiler.reportPath=*.log
sonar.cxx.compiler.charset=UTF-8
sonar.cxx.compiler.regex=^.*>(?<filename>.*)\\((?<line>[0-9]+)\\):\\x20warning\\x20(?<id>C\\d\\d\\d\\d):(?<message>.*)$
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
