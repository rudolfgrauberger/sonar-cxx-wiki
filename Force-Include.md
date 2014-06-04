The C++ community plugin provides "force-including" of header files. This method of “force-including” files is sometimes a useful way of defining macros, types or compiler built-ins.

This configuration property has the same effect as specifying the file with double quotation marks in an #include directive on the first line of every source file. If you add multiple files they are included in the order they are listed from left to right.

The first directory searched for file is the preprocessor's working directory instead of the directory containing the main source file. If not found there, it is searched for in the remainder of the ‘#include "..."’ search chain as normal (sonar.cxx.includeDirectories).

**See also**
* GCC --include,
* Visual Studio /FI or
* cppcheck --include

**Example: VS10Macros.h, MyMacros.h**

```
sonar.cxx.forceIncludes=VS10Macros.h,MyMacros.h
```

Original source code file:
```C++
// Comment
#include "stdafx.h"
#include "..."
...
// your source code ...
```

Resulting source code file:
```C++
#include "VS10Macros.h"
#include "MyMacros.h"
// Comment
#include "stdafx.h"
...
#include "..."
// your source code ...
```
