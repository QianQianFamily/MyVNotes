# VS tips
[How to use #pragma](https://docs.microsoft.com/en-us/cpp/preprocessor/pragma-directives-and-the-pragma-keyword?view=vs-2017)
[Predefined Macro](https://docs.microsoft.com/en-us/cpp/preprocessor/predefined-macros?view=vs-2017)


## NDEBUG
NDebug is a standard macro with the semantic "Not Debug" for C89, C99, C++98, C++2003, C++2011, C++2014 standards. There are no _DEBUG macros in the standards.  
Visual Studio defines _DEBUG when you specify the /MTd or /MDd option.
Unfortunately "DEBUG" is overloaded heavily. For instance, it's recommended to always generate and save a pdb file for RELEASE builds. Which means one of the -Zx flags, and -DEBUG linker option. While _DEBUG relates to special debug versions of runtime library such as calls to malloc and free. Then NDEBUG will disable assertions.