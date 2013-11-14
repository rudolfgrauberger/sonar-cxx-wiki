### Gcov / gcovr

1. Make sure to compile and link with the ```--coverage``` flag. Disable optimizations and switch on debugging.
2. Execute your application / your tests. This will generate .gcda-files.
3. Collect the coverage information and generate the report using gcovr:
```BASH 
gcovr -x -r . > report.xml
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