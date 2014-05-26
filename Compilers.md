The Community C++ Plugin supports feeding compiler warnings as violations into SonarQube. Here is a quick guide how to run the supported compilers and catch needed relevant output.

### GNU C++ Compiler
TODO @typz or @wenns

### Microsofts Visual Compiler
The Compiler sensor consumes the warning messages available in the MS build log. A regular expression can be configured to extract the information for SonarQube.

```
sonar.cxx.compiler.parser=Visual C++
sonar.cxx.compiler.reportPath=*.log
sonar.cxx.compiler.charset=UTF-8
sonar.cxx.compiler.regex=^.*>(?<filename>.*)\\((?<line>[0-9]+)\\):\\x20warning\\x20(?<id>C\\d\\d\\d\\d):(?<message>.*)$
```
 
Preconditions:
- set option for 'Project and Solutions -> Build and Run': MSBuild Project build log verbosity = Normal
- enable code analysis on build (per *.vcxproj property or on cpp user property page). This feature is available in premium or ultimate VS edition.

A typical log file for MSVC 11.0/12.0 will contain Compiler warnings shown in the following excerpt:
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
  