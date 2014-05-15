C++ community plugin implements a C++03 and C++11 compatible grammar. Additional below listed compiler specific extensions are supported:

###Preprocessor

**With GCC'S it is allowed to leave the variable argument out entirely**

Example:
```C++
#define eprintf(format, ...) fprintf (stderr, format, __VA_ARGS__)
eprintf("success!");
```
Results in:
```C++
fprintf(stderr, "success!", );
```


###Parser

**GCC's statement expression**

A compound statement enclosed in parentheses may appear as an expression in GCC. This allows you to use loops, switches, and local variables within an expression. 

Example:
```C++
#define maxint(a,b) \
       ({int _a = (a), _b = (b); _a > _b ? _a : _b; })
```


**GCC's Conditionals with Omitted Operands**

There is a GCC extension which allows the middle operand in a conditional expression to be omitted. Therefore, the expression 'x ? : y' has the value of x if that is nonzero; otherwise, the value of y.

Example:
```C++
... = x ? : y;
```


**Microsoft Visual Studio Attributted ATL support**

There is a special flavor of ATL called 'Attributed ATL' or ATL and Attributes. The attributes were added to make programming ATL simpler. The attributes would typically lead to source code insertion.

Example:
```C++
[
    object,
    uuid("2543548B-EFFB-4CB4-B2ED-9D3931A2527D"),
    dual,
    oleautomation,
    nonextensible,
    hidden,
    helpstring("IServicesMgr Interface"),
    pointer_default(unique)
]
__interface IMyInterface : IDispatch
{
  [id(1), helpstring("method Start")] HRESULT Start([in] BSTR ServiceName);
  [id(2), helpstring("method Stop")] HRESULT Stop([in] BSTR ServiceName);
};
```
