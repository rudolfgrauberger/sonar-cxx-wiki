C++ community plugin implements a C++03 and C++11 compatible grammar but most compilers support additional compiler specific extensions. To get no syntax errors and meaningful results you have to workaround these extensions.

To keep the compiler grammer as simple as possible it was a conscious design to support such extensions mainly with marco definitions and not an extension of the grammar.

Some examples for compiler specific extensions:
* list with [Microsoft-Specific Modifiers](http://msdn.microsoft.com/en-us/library/6bh0054z.aspx)
* tbd list with GCC-Specific Modifiers

In the description below you find some typical practices to mock the extensions or to replace them with supported alternatives.

Additional data types are typically replaces with known data types:
```C++
#define __int32 int
__int32 n=0;
```
after preprocessing this will result in:
```C++
int n=0;
```
Things like additional function calling conventions should be mocked:
```C++
#define __stdcall
void __stdcall example() {
}
```
after preprocessing this will result in:
```C++
void example() {
}
```
For more complex attributes often variadic macros provide a solution:
```C++
#define __declspec(...)
__declspec(align(32)) struct example {
   int a;
};
```
after preprocessing this will result in:
```C++
struct example {
   int a;
};
```
There are two ways to add preprocessor directives to the C++ community plugin. Via the ```sonar.cxx.defines``` or the ```sonar.cxx.forceInclude``` configuration property, see [[Supported configuration properties]] for details. In most cases it is easier to write once a header file for the target build environment and reuse this header file with force include in all projects.