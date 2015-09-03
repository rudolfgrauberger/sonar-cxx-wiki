In case of problems it is often helpful to turn debug information on. This will add more detailed information to stdout or the log files.

**Step 1:** Produce execution **debug output**

```
sonar-runner -X ...
-X,--debug Produce execution debug output
```
Second option is -e to give you execution error messages:
```
sonar-runner -e ...
-e,--errors Produce execution error messages
```


**Step 2:** Control level of logs

If you need more debug information you can add the ```sonar.verbose``` property by adding the command line parameter ```-Dsonar.verbose=true```.

```
sonar-runner -X -Dsonar.verbose=true ...
```

 There is also the ```sonar.log.level``` which controls the quantity / level of logs produced during an analysis. ```sonar.verbose``` activates DEBUG mode for the analyzer. This is a shortcut of ```sonar.log.level=DEBUG```.
* ```sonar.log.level=DEBUG```: Display INFO logs + more details at DEBUG level. Similar to ```sonar.verbose=true```
* ```sonar.log.level=TRACE```: Display DEBUG logs + all the SQL queries + their timings executed by the analyzer. Similar to ```sonar.showProfiling=FULL```
* you can combine the flags, e.g. ```sonar.log.level=TRACE|DEBUG```
* ```sonar.showProfiling``` is deprecated since 5.1, replaced by ```sonar.log.level=TRACE|DEBUG```


**Step 3:** Redirect output to a LOG file

By default the output is written to stdout. Errors are written to stderr. For analysis purpose it is recommended to redirect both to a LOG file.

Microsoft Windows:
```
sonar-runner -X -e -Dsonar.verbose=true ... > sonar-runner.log 2>&1
```
