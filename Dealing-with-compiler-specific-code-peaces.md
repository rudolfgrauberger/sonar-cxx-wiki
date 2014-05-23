C++ community plugin implements a C++03 and C++11 compatible grammar but most compilers support additional compiler specific extensions. To get no syntax errors and meaningful results you have to workaround these extensions.

To keep the compiler grammer as simple as possible it was a conscious design decision to support such extensions mainly with marco definitions and not an extension of the grammar. There are only some exceptions to this, where preprocessor directives won't work, see [[Supported compiler specific extensions]].

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

To get an overview about available compiler specific extensions the links below can help you:
* [Microsoft-Specific Modifiers](http://msdn.microsoft.com/en-us/library/6bh0054z.aspx)
* [GNU compiler extensions to the C++ language](http://gcc.gnu.org/onlinedocs/gcc-4.9.0/gcc/C_002b_002b-Extensions.html)

###Example: Microsoft-specific extensions###

For Visual Studio 2010 there is an example how to deal with the compiler specific extension. You can use this as an template for your own adaptions.

[Visual Studio 2010 example header file](https://github.com/wenns/sonar-cxx/blob/master/sonar-cxx-plugin/src/main/resources/macros/VS10Macros.h)

To use the header file you have to edit some settings corresponding to your compiler settings:

1) Is your project an application (none), a DLL(_DLL) or a static library (_LIB)?
```
#define _DLL 1
//#define _LIB 1
```

2) Is your project a Windows (_WINDOWS) or Console (_CONSOLE) application?
```
#define _WINDOWS 1
//#define _CONSOLE 1
```

3) Does your project use Unicode (UNICODE) or Multi-Byte (_MBCS) character set
```
#define UNICODE 1
#define _UNICODE 1
//#define _MBCS 1
```

4) Are you using the MFC?
<br>Build Settings for an MFC DLL
- Regular, statically linked to MFC: _WINDLL, _USRDLL
- Regular, using the shared MFC DLL: _WINDLL, _USRDLL, _AFXDLL
- Extension DLL: _WINDLL, _AFXDLL, _AFXEXT
```
//#define _WINDLL 1
//#define _USRDLL 1
#define _AFXDLL 1
//#define _AFXEXT 1
```

5) Are you using the ATL?
- Dynamic Link to ATL: _ATL_DLL
- Static Link to ATL: _ATL_STATIC_REGISTRY
```
#define _ATL_DLL 1
//#define _ATL_STATIC_REGISTRY 1
```

6) Add your other preprocessor definitions
<br>Copy your settings from the visual studio project (Project\Properties\Configuration Properties\C/C++\Preprocessor). Have also a look to the 'Inherited values' (Edit\Inherited values).

7) Include the header file with [[Force Include]].
