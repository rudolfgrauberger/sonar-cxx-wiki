The Community C++ Plugin supports feeding compiler warnings as violations into SonarQube. Here is a quick guide how to run the supported compilers and catch needed relevant output.

### GNU C++ Compiler
To feed GCC warnings into SonarQube, make sure to:

1. Capture the warnings from your build into a file (e.g build.log) using shell redirections or similar
2. Set according property: ```sonar.cxx.compiler.reportPath=build.log```
3. Activate the rules from the rule repository "compiler-gcc"
4. Run the analysis

### Microsofts Visual Studio Compiler

The compiler sensor consumes the warning messages available in the build log. Depending on the configuration properties there are more or less warning available.

**Visual Studio settings**

* To create the warnings you have to activate the following configuration properties. Open the project property page with ```Project\Properties```. Select ```Configuration Properties\C/C++\General``` and set ```Warning Level``` to ```Level3``` or ```Level4```.

* Enable Code Analysis on Build. This feature is available in Premium or Ultimate editions only. Select ```Configuration Properties\Code Analysis\General```, activate ```Enable Code Analysis on Build```. As default you can use ```Microsoft Native Recommended Rules```.

![MSVS cpp.user-propery-pages](https://cloud.githubusercontent.com/assets/2315215/3085369/b7b3f4d4-e50f-11e3-8e9e-6d1712db1320.PNG)

A regular expression can be configured to extract the information for SonarQube:
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
  