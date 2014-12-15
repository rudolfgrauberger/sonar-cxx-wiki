In case of problems it is often helpful to turn debug information on. This will add more detailed information to stdout or the log files.

**Step 1:** Produce execution **debug output**

```
sonar-runner -X ...
-X,--debug Produce execution debug output
```

**Step 2:** If you need more debug information you can add the **sonar.verbose** property by adding the command line parameter -Dsonar.verbose=true.

```
sonar-runner -X -Dsonar.verbose=true ...
```