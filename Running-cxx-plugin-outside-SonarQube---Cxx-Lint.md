Here we are referring to the rules provided by the plugin, they can be found under the repository ```c++ SonarQube```. **This does not refer to external tools like cppcheck**

# Rationale
Run Cxx checks before committing code, following same approach as SonarLint in visual studio or eclipse.

# Requirements
Java 7 or above is installed.

# Installation and configuration
The linter can be download from your SonarQube instance, using the following address: http://localhost:9000/static/cxx/cxx-lint-0.9.5.jar. In this case your SonarQube instance is installed in http://localhost:9000 and the Cxx Plugin version 0.9.5 is installed in server. In case a different version is installed, cxx-lint-0.9.5.jar will become cxx-lint-0.9.6.jar, cxx-lint-0.9.7.jar, etc.

Drop the jar in some place that you have access, for example. c:\tools\cxx-lint-0.9.5.jar

# Execution
```
java -jar c:\tools\cxx-lint-0.9.5.jar -f E:\SRC\DIR\tool.cpp
```

This will produce this kind of syntax:

```
E:\SRC\DIR\tool.cpp(390): Warning : sscanf can be ok, but is slow and can overflow buffers.  [overflow]
```

# Configuring rules to the linter
Its possible to define a settings file and pass to the linter to configure the rules or to pass C++ compilation settings. The following format is expected for a VC++ environment.
```
{
  "platformToolset": "V120", 
  "platform": "Win32",
  "projectFile": "D:/prod/dir/project.vcxproj",
  "includes": [
    "C:/Program Files (x86)/Microsoft Visual Studio 12.0/VC/INCLUDE",
    "C:/Program Files (x86)/Microsoft Visual Studio 12.0/VC/ATLMFC/INCLUDE",
    "C:/Program Files (x86)/Windows Kits/8.1/include/shared",
    "C:/Program Files (x86)/Windows Kits/8.1/include/um",
    "C:/Program Files (x86)/Windows Kits/8.1/include/winrt",
    "D:/prod/structures/Packages/gtestmock.1.7.5/build/native/include/",
    "D:/prod/structures/Packages/gtestmock.1.7.5/build/native/include/googletest"
  ],
  "defines": [
    "_MBCS",
    "GTEST_LINKED_AS_SHARED_LIBRARY=1",
    "NO_WARN_MBCS_MFC_DEPRECATION",
    "NT",
    "OS_NT",
    "WIN32",
    "_WIN32_WINNT=0x0601",
    "WINVER=0x0601"
  ],
  "additionalOptions": [
    "/Zc:strictStrings",
    "-Zm200",
    "-D_CRT_SECURE_NO_DEPRECATE",
    "-w34063",
    "-w34189",
    "-w34206",
    "-w34327",
    "-w34701",
    "/Zc:rvalueCast",
    "/Zc:inline"
  ],
  "rules": [
    {
      "ruleId": "ParsingErrorRecovery",
      "status": "Enabled"
    },
    {
      "ruleId": "CollapsibleIfCandidate",
      "status": "Enabled"
    },
    {
      "ruleId": "FileName",
      "status": "Enabled",
      "properties": {
        "format": "(([a-z_][a-z0-9_]*)|([A-Z][a-zA-Z0-9]+))$"
      }
    },
    {
      "ruleId": "FixmeTagPresence",
      "status": "Enabled"
    },
    {
      "ruleId": "TabCharacter",
      "status": "Enabled",
      "properties": {
        "createLineViolation": "false"
      }
    }
  ]
}
```

For environments other than unix, the additionalOptions do no apply. projectFile can also be skipped in this case. All parameters are optional.
Rules defined in configuration file will be run, all other will be skipped.
Properties for the rules can be obtained in the Quality profile when setting the parameter.

To execute pass the argument -s settings file to the jar like this
```
java -jar c:\tools\cxx-lint-0.9.5.jar -f E:\SRC\DIR\tool.cpp -s settings.json
```

# Using this in Visual Studio
If you use Visual Studio, you are in luck. you can install the VSSonarExtension https://visualstudiogallery.msdn.microsoft.com/7fc312c3-f1ab-49f8-b286-dbf7fff37305 that implements this logic.



