In case of problems it is often helpful to turn debug information on. This will add more detailed information to stdout or the log files.

**Step 1:** Produce execution **debug output**

```
sonar-runner -X ...
-X,--debug Produce execution debug output
```

**Step 2:** Control level of logs

If you need more debug information you can add the ```sonar.verbose``` property by adding the command line parameter ```-Dsonar.verbose=true```.

```
sonar-runner -X -Dsonar.verbose=true ...
```

 There is also the `sonar.log.level` which controls the quantity / level of logs produced during an analysis. `sonar.verbose` activates DEBUG mode for the analyzer. This is a shortcut of `sonar.log.level=DEBUG`.
* `sonar.log.level=DEBUG`: Display INFO logs + more details at DEBUG level. Similar to `sonar.verbose=true`
* `sonar.log.level=TRACE`: Display DEBUG logs + the timings of all ElasticSearch queries and Web API calls executed by the SonarQube Scanner.
* `sonar.showProfiling=true/false`: Display logs to see where the analyzer spends time. This parameter is generating a file containing these timing infos in <workingDir>/profiling/<moduleKey>-profiler.xml where <workingDir> is:
   * sonar/profiling/ when analysis is run with Sonar Scanner
   * target/sonar/profiling/ when Maven is used 
* you can combine the flags, e.g. ```sonar.log.level=TRACE|DEBUG```
* `sonar.scanner.dumpToFile`: Outputs to the specified file the full list of properties passed to the scanner API as a means to debug analysis.

**Step 3:** Redirect output to a LOG file

By default the output is written to stdout. Errors are written to stderr. For analysis purpose it is recommended to redirect both to a LOG file.

Microsoft Windows command line:
```
sonar-runner -X -Dsonar.verbose=true ... > sonar-runner.log 2>&1
```
Linux bash:
```
sonar-runner -X -Dsonar.verbose=true ... &> sonar-runner.log
```
