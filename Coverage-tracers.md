### Gcov / gcovr

1. Make sure to compile and link with the ```--coverage``` flag. Disable optimizations and switch on debugging.
2. Execute your application / your tests. This will generate .gcda files.
3. Execute gcov to use the .gcda files precedently generated, it will generate .gcov files somewhere you define.
4. Collect the coverage information and generate the report using gcovr:
```BASH
gcovr -x --object-directory=ABSOLUTE_PATH_TO_GCOV_FILES_FOLDER > report.xml
```
### Bullseye
Create the XML coverage report with:
```BASH
covxml -f UTCoverage.cov -o bullseyecoverage-result-0.xml
```

To merge two coverage files (e.g. to obtain the overall coverage):
```BASH
covmerge -c ITCoverage.cov UTCoverage.cov -f ALLCOVERAGE.cov
````

### Microsofts Code Coverage

***Prerequisites***
* Visual Studio Premium or Visual Studio Ultimate 2010, 2012 or 2013
* MSDN: [Using Code Coverage to Determine How Much Code is being Tested](http://msdn.microsoft.com/de-de/library/dd537628.aspx)
* With Visual Studio 2012 the file CodeCoverage.exe is normally located in 'C:\Program Files (x86)\Microsoft Visual Studio 11.0\Team Tools\Dynamic Code Coverage Tools'.
* With Visual Studio 2013 the file CodeCoverage.exe is normally located in 'C:\Program Files (x86)\Microsoft Visual Studio 12.0\Team Tools\Dynamic Code Coverage Tools'.
* The *CodeCoverage.exe* runs as master of the unit test runner.

Creating the coverage report for SonarQube is a two step process:

***(1) Generate a coverage file with:***
```
CodeCoverage.exe collect /output:out.coverage [...]
```
where [...] is your test client. Example below is for Visual Studio:
```
mstest.exe /testmetadata:.\some.vsmdi /testlist:03_COMP_smoke/clientAndServer/pass /runconfig:.\localtestrun2010.testrunconfig /resultsfile:testResults.trx
```

***(2) Convert the resulting coverage file into an XML file:***
```
CodeCoverage.exe analyze /output:result.xml out.coverage
```
With this option it is also possible to merge several coverage results into one XML file.
```
CodeCoverage.exe analyze /output:result.xml out1.coverage out2.coverage
```

***(3) Read coverage file with SonarQube***

Define the location of your coverage file in the SonarQube configuration file (sonar.cxx.coverage.reportPath) and start the sonar runner to read it.

**Hints:**
* Problems are mostly path problems. Ensure that the source files defined in your report file exist on the machine you are running the sonar runner. Paths in report file could be absolute or relative to configuration file (.\\...).
* [Customizing Code Coverage Analysis](http://msdn.microsoft.com/en-us/library/jj159530.aspx)
* [Troubleshooting Code Coverage](http://msdn.microsoft.com/en-us/library/jj159523.aspx)
