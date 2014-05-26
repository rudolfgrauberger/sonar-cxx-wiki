The Community C++ Plugin supports feeding compiler warnings as violations into SonarQube. Here is a quick guide how to run the supported compilers and catch needed relevant output.

### GNU C++ Compiler
TODO @typz or @wenns

### Microsofts Visual Compiler
The Compiler sensor consumes the warning messages available in the build log. 
preconditions:
- set option for 'Project and Solutions -> Build and Run': MSBuild Project build log verbosity = Normal
- enable code Analysis on build (per *.vcxproj property or on cpp user property page)
  