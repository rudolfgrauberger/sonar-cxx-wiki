C++ community plugin implements a C++03 and C++11 compatible grammar. Additional below listed compiler specific extensions are supported:

###Preprocessor

**With GCC's it is allowed to leave the variable argument out entirely**

Example:
```C++
#define eprintf(format, ...) fprintf (stderr, format, __VA_ARGS__)
eprintf("success!");
```
Results in:
```C++
fprintf(stderr, "success!", );
```

**GCC's special meaning of token paste operator**

If variable argument is left out then the comma before the paste operator will be deleted.

Example:
```C++
#define eprintf(format, ...) fprintf (stderr, format, ##__VA_ARGS__)
eprintf("success!");
```
Results in:
```C++
fprintf(stderr, "success!");
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

**GCC's Case Ranges**

You can specify a range of consecutive values in a single case label, like this: ```case low ... high:```. This has the same effect as the proper number of individual case labels, one for each integer value from low to high, inclusive. Be careful: Write spaces around the ..., for otherwise it may be parsed wrong when you use it with integer values. For example, write this: ```case 1 ... 5:``` rather than this: ```case 1...5:```.

Example:
```C++
switch(c) {
   case 'A' ... 'C':
      break;
}
```

**ISO C99: Designated Initializers**

In ISO C99 you can give the elements in any order, specifying the array indices or structure field names they apply to

Example:
```C
int a[6] = { [4] = 29, [2] = 15 }; // is equivalent to: int a[6] = { 0, 0, 15, 0, 29, 0 };
```

GCC's extension: To initialize a range of elements to the same value, write ‘[first ... last] = value’.

Example:
```C
int widths[] = { [0 ... 9] = 1, [10 ... 99] = 2, [100] = 3 };
```

In a structure initializer, specify the name of a field to initialize with ‘.fieldname =’ before the element value.

Example:
```C
struct point { int x, y; };
struct point p = { .y = yvalue, .x = xvalue };
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