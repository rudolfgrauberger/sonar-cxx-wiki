The plugin has three very universal checks to create custom rules. Optional for all rules an Ant-style matching pattern (matchFilePattern) for the path can be defined.

Following matchFilePattern rules are applied:
```
? matches single character
* matches zero or more characters
** matches zero or more 'directories'
use always '/' as a directory separator
there must always be a root directory
```

Some examples of path patterns:
```
/**/*.cpp - matches all .cpp files in all directories (you have to define the root directory '/'), e.g. org/Foo.cpp or org/foo/Bar.cpp or org/foo/bar/Baz.cpp
/**/test/**/Foo.cpp - matches all 'Foo.cpp' files in directories with one 'test' directory in the path, e.g. org/test/Foo.cpp or org/bar/test/bar/Foo.cpp
org/T?st.cpp - matches org/Test.cpp and also org/Tost.cpp
org/*.cpp - matches all .cpp files in the org directory, e.g. org/Foo.cpp or org/Bar.cpp
org/** - matches all files underneath the org directory, e.g. org/Foo.cpp or org/foo/bar.jsp
org/**/Test.cpp - matches all Test.cpp files underneath the org directory, e.g. org/Test.cpp or org/foo/Test.cpp or org/foo/bar/Test.cpp
org/**/*.cpp - matches all .cpp files underneath the org directory, e.g. org/Foo.cpp or org/foo/Bar.cpp or org/foo/bar/Baz.cpp
```

## XPath rule
This rule allows to define C++ rules with help of an XPath expression.

The rules must be written in [XPath](http://en.wikipedia.org/wiki/XPath) (version 1.0) to navigate the language's [Abstract Syntax Tree](http://en.wikipedia.org/wiki/Abstract_syntax_tree) (AST). For the plugin an SSLR Toolkit is provided to help you navigate the AST. Each language's SSLR Toolkit is a standalone application that displays the AST for a piece of code source that you feed into it, allowing you to read the node names and attributes from your code sample and write your XPath expression. Knowing the XPath language is the only prerequisite, and there are a lot of tutorials on XPath online (see http://www.w3schools.com/xpath/ for example).

The proper SSLR Toolkit can be downloaded from here (TODO).

Violations are created depending on the return value of the XPath expression. If the XPath expression returns:
* a single or list of AST nodes, then a line violation with the given message is created for each node
* a boolean, then a file violation with the given message is created only if the boolean is true
* anything else, no violation is created

Example: Create a warning if an identifier is shorter than 3 signs.

```C++
matchFilePattern = "";
xpathQuery = "//IDENTIFIER[string-length(@tokenValue)<3]";
message = "Use more meaningful identifiers!";
```

```C++
void test()
{
  int i; // warning: Use more meaningful identifiers!"
  int value;
}
```

## File RegEx rule
This rule can be used to create rules which will be triggered when a file matches a given regular expression.
For each matching file a violation will be created. All Java regular expressions are supported, for a description see [here](http://docs.oracle.com/javase/7/docs/api/java/util/regex/Pattern.html).

## Line RegEx rule
This rule can be used to create rules which will be triggered when a line matches a given regular expression.
For each matching line a violation will be created. All Java regular expressions are supported, for a description see [here](http://docs.oracle.com/javase/7/docs/api/java/util/regex/Pattern.html).

Example:

```C++
matchFilePattern = "/**/*.h"; // all files with .h file extension
regularExpression = "#include\\s+\"stdafx\\.h\"";
message = "Found '#include "stdafx.h"' in a header file!";
```

```C++
#include "stdafx.h" // warning "Found '#include "stdafx.h"' in a header file!"

class MyClass {
};
```
