Here is a quick guide how to run the supported analyzers and generate reports such that it fits SonarQube's needs.

**IMPORTANT**: Quality rules have to be activated in order to enable the import of warnings. Please see [Activate quality rules](https://github.com/SonarOpenCommunity/sonar-cxx/wiki/Activate-quality-rules) for more info.

### Cppcheck

In order to run Cppcheck and generate a fitting report, make sure:

* to call it from the projects root directory
* to pass all include directories (using _-I \<path\>_) as otherwise the analysis will be incomplete
* that the <sources> parameter matches the **sonar.sources** list in _sonar-project.properties_
* to create a XML-report using the parameter ```--xml-version=2``` for version 2 or ```--xml``` for version 1. Both versions are supported, version 2 is the default.
* to get the report from the standard error channel

Example command line:

```BASH
cppcheck --xml file1.cpp 2> report.xml
cppcheck --xml-version=2 file1.cpp 2> report.xml

cppcheck -v --enable=all --xml -I[include directory] [sources] 2> report.xml
```
Example report files:

**V1:**
```XML
<?xml version="1.0"?>
<results>
  <error file=".\file1.cpp" line="123" id="someError"
               severity="error" msg="some error text"/>
</results>
```

**V2:**
```XML
<?xml version="1.0" encoding="UTF-8"?>
<results version="2">
   <cppcheck version="1.53">
      <errors>
         <error id="someError" severity="error" msg="short error text"
                    verbose="long error text" inconclusive="true">
            <location file=".\file1.cpp" line="1"/>
         </error>
      </errors>
</results>
```

A Cppcheck run may take a while on a big code base. To cut down analysis times, check the following options:

* Use ```-j N``` option to run _N_ workers in parallel
* Use only checks you're interested in via the option ```_--enable=<check>_```
* Restrict checking of preprocessor configurations using the options ```-D -U```
* Start with project include folders (-I) without system include folders. System include folders and include folders of big libraries like Boost, XERXES, ... make Cppcheck run much slower.
* Get a faster machine ;)

To extend the set of known Cppcheck rules see [[Extending the code analysis]].

### Valgrind
SonarQube can be fed with results of a Valgrind/Memcheck analysis. That's very valuable because:
* due to its dynamic nature, the false positives rate is very low (Given good maintained suppression files, of course)
* it is able to find serious issues which are often hard to detect otherwise

Just tell Valgrind to generate XML output. The 'tool' option isn't necessary as 'memcheck' is the default one. Make sure the binaries contain debug info. The actual call should look something like:

```BASH
valgrind --xml=yes --xml-file=report.xml <program> <arguments>
```

To extend the set of known Valgrind rules see [[Extending the code analysis]].

### Vera++
Vera++ does static C++ code checking, focusing mostly on style issues. There are two possibilities to create a report.

Newer versions of Vera++ support the ```--checkstyle-report (-c)``` command line option to create a Checkstyle XML report:
```BASH
vera++ -s -c vera3.xml main.cxx
```

Another possibility with older versions is to convert the output wit a Perl script. To feed Vera++ analysis results into SonarQube:
* Find all the files we want to be analysed
* Pipe this list into Vera++ and
* Pipe the resulting output into a Perl script which finally generates the required XML.

Altogether:

```BASH
find <path> -regex ".*\.cc\|.*\.hh" | vera++ - -showrules -nodup |& vera++Report2checkstyleReport.perl > report.xml
```

An example output could looks like this:
```XML
<?xml version="1.0" encoding="UTF-8"?>
<checkstyle version="5.0">
  <file name="main.cxx">
    <error source="T013" severity="info" line="1" message="no copyright notice found" />
    <error source="T011" severity="info" line="2" message="closing curly bracket not in the same line or column" />
  </file>
</checkstyle>
```

To extend the set of known Vera++ rules see [[Extending the code analysis]].

### RATS
RATS stands for "Rough Auditing Tool for Security". This tool performs static C++ code checks focusing mainly on security issues. Just tell it to create XML output and redirect the standard channel into a file:

```BASH
rats -w 3 --xml <sources> > report.xml
```
To extend the set of known RATS rules see [[Extending the code analysis]].

### PC-lint
The PC-lint XML output needs to be formatted to fit SonarQube.

```
// XML options for SONAR.
-v // Turn off verbosity
-width(0,0) // Don't break long lines
+xml(?xml version="1.0" ?) // add version information
+xml(results) // Turn on XML escapes
-"format=<issue file =\q%f\q line = \q%l\q number = \q%n\q desc = \q%m\q/>"
-"format_specific= "
-hFs1 // The height of a message should be 1 i.e. don't output the line in error
-e900 // 'Successful completion message'
```

This formatting has been verified with PC-lint 9.0k. For further details on how to configure PC-lint please refer to [product page](http://www.gimpel.com/html/pcl.htm).

To extend the set of known PC-lint rules see [[Extending the code analysis]].

_Note: Rules for this tool are disabled by default, so they need to be enabled in the relevant quality profile before they can be imported into SonarQube._

### Dr. Memory
SonarQube can be fed with results of a [Dr. Memory](http://drmemory.org/) analysis.

Just launch your program with **Dr. Memory**. The actual call should look something like:

```BASH
drmemory.exe -logdir c:/logs -- c:/path/to/my/app
```
Now, you just have to fill the **sonar.cxx.drmemory.reportPath**:

```BASH
sonar.cxx.drmemory.reportPath=c:/logs/**/results.txt
```

The results.txt file should look something like:

```BASH
Dr. Memory version 1.8.0 build 8 built on Sep  9 2014 16:27:02
Dr. Memory results for pid 1952: "Mask.Acceptance.Tests.exe"
Application cmdline: "Mask.Acceptance.Tests.exe"
Recorded 108 suppression(s) from default C:\Program Files (x86)\Dr. Memory\bin\suppress-default.txt

Error #1: UNINITIALIZED READ: reading register eax
# 0 ImageElementParser::Parse                                                 [r:\developpement\mask\peage\api_masque\sources\maskcpp\core\parsing\imageelementparser.cpp:21]
# 1 MRTComponentsParser::Parse                                                [r:\developpement\mask\peage\api_masque\sources\maskcpp\core\parsing\mrtcomponentsparser.cpp:47]
# 2 MRTPageParser::Parse                                                      [r:\developpement\mask\peage\api_masque\sources\maskcpp\core\parsing\mrtpageparser.cpp:13]
# 3 MRTFileParser::Parse                                                      [r:\developpement\mask\peage\api_masque\sources\maskcpp\core\parsing\mrtfileparser.cpp:22]
# 4 MRTMasqueParserAdapter::Parser                                            [r:\developpement\mask\peage\api_masque\sources\maskcpp\core\parsing\mrtmasqueparseradapter.cpp:12]
# 5 Mask::Load                                                                [r:\developpement\mask\peage\api_masque\sources\maskcpp\core\mask.cpp:15]
# 6 Mask::Load                                                                [r:\developpement\mask\peage\api_masque\sources\maskcpp\core\mask.cpp:8]
# 7 BitmapGenerationConfiguration::AndGetResultAsBmpContent                   [r:\developpement\mask\peage\api_masque\sources\maskcpp\factory\maskfactory.h:72]
# 8 MaskAcceptanceTest::LaunchTest                                            [r:\developpement\mask\peage\api_masque\tests\acceptance\acceptancetestexecutor.cpp:68]
# 9 conditions::Conditions_OnImage_Test::TestBody                             [r:\developpement\mask\peage\api_masque\tests\acceptance\conditionstest.cpp:44]
#10 testing::internal::HandleSehExceptionsInMethodIfSupported<>               [r:\developpement\mask\build\packages\external.google-test.1.6.2-dev\sources\src\gtest.cc:2075]
#11 testing::internal::HandleExceptionsInMethodIfSupported<>                  [r:\developpement\mask\build\packages\external.google-test.1.6.2-dev\sources\src\gtest.cc:2126]
#12 testing::Test::Run                                                        [r:\developpement\mask\build\packages\external.google-test.1.6.2-dev\sources\src\gtest.cc:2162]
#13 testing::TestInfo::Run                                                    [r:\developpement\mask\build\packages\external.google-test.1.6.2-dev\sources\src\gtest.cc:2338]
#14 testing::TestCase::Run                                                    [r:\developpement\mask\build\packages\external.google-test.1.6.2-dev\sources\src\gtest.cc:2445]
#15 testing::internal::UnitTestImpl::RunAllTests                              [r:\developpement\mask\build\packages\external.google-test.1.6.2-dev\sources\src\gtest.cc:4237]
#16 testing::internal::HandleSehExceptionsInMethodIfSupported<>               [r:\developpement\mask\build\packages\external.google-test.1.6.2-dev\sources\src\gtest.cc:2075]
#17 testing::internal::HandleExceptionsInMethodIfSupported<>                  [r:\developpement\mask\build\packages\external.google-test.1.6.2-dev\sources\src\gtest.cc:2126]
#18 testing::UnitTest::Run                                                    [r:\developpement\mask\build\packages\external.google-test.1.6.2-dev\sources\src\gtest.cc:3874]
#19 main                                                                      [r:\developpement\mask\build\packages\external.google-test.1.6.2-dev\sources\src\gtest_main.cc:38]
Note: @0:00:11.965 in thread 1804
Note: instruction: test   %eax %eax
```

### Clang Static Analyzer

Plist output format generated by the [Clang Static Analyzer](https://clang-analyzer.llvm.org/) can be parsed and processes by the plugin.

#### Use Clang to analyze simple files

A simple file can be analyzed like this.  
Run clang from your project root.

Select the plist as an output format. To generate the plist output there are two options:
* `-analyzer-output plist`
* `-analyzer-output plist-multi-file`

Both options will generate a report file in plist format. The difference is that in the case of `plist-multi-file` bug reports across multiple files will be generated if the bug execution path goes through multiple files. For example: the issue is in a function in a header file called from a cpp file. In this case the report will contain the relevant parts from the cpp file too to help to understand the reported issue (analyzer assumptions during the analysis on a possible execution path).

```sh
clang -cc1 -analyze -analyzer-checker=core.DivideZero src/divzero.cc -I src -analyzer-output plist-multi-file -o divzero.plist
```

To list the available checkers use this command:  
```sh
$ clang -cc1 -analyzer-checker-help
```

See help for further details on how to configure the analysis.
```sh
$ clang -cc1 --help
```

Add this configuration to the `sonar-project.properties` file to import the generated plist report:
```
sonar.cxx.clangsa.reportPath=divzero.plist
```

#### Use scan-build to analyze a project

To run the static analysis on your project the [scan-build](https://clang-analyzer.llvm.org/scan-build.html) tool can be used.

There is an alternative rewritten version of the original tool which is available [here](https://github.com/rizsotto/scan-build). See the used guide how to install the tool and for further usage examples configuration options.

Run scan-build in your project root.

In the example I assume you are using the [rewritten version](https://github.com/rizsotto/scan-build) to analyze your project:
```
scan-build -plist --intercept-first --analyze-headers -o analyzer_reports make
```

Add this configuration to the `sonar-project.properties` file to import the generated plist reports:
```
sonar.cxx.clangsa.reportPath=analyzer_reports/*/*.plist
```

### Clang Tidy
Please use the properties...
```propertis
sonar.cxx.clangtidy.reportPath=
sonar.cxx.clangtidy.customRules= #optional
sonar.cxx.clangtidy.charset=     #optional
```

...in order to import the clang-tidy reports.