C++ community plugin implements a C++03 and C++11 compatible grammar. Additional below listed compiler specific extensions are supported:

###Preprocessor


###Parser

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
