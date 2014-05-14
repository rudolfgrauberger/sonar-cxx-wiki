To get meaningful *SonarQube* results your code should be syntactically correct code. The C++ community plugin has error recovery on declaration level, but do not expect as much guidance as you can get from a C++ compiler.

**Error recovery:**
* Syntax errors within a declaration are skipped, analysis is continued with next declaration.
* For erroneous declarations the parser output the file, line number and closest identifier during analyzer run (e.g. sonar-runner).
* Rule to detected skipped code do support you to find issues: Enable 'Sonar \ C++ skip parser error' in your *Quality Profile*.

**Example:**
```C++
01: int i=0;
02: 
03: void func1()
04: {
05:    i=1 //;
06: }
07:
08: void func2()
09: {
10:    i=2;
11: }
```

The parser will find a syntax error in line 5 (missing semicolon). This results in a syntax error in the *func1* declaration. You will get the error message below. The parser ignores the whole declaration starting from line 3 and ending with line 6. The parser continues with analysis in line 7 (*func2* is analyzed again). 

```
15:54:45.567 WARN  - [example.cpp:3]: syntax error, skip 'func1'
```