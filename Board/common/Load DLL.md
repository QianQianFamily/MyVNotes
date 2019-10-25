# 主要函数


- LoadLibrary
- GetProcAddress
- FreeLibrary

## cstlib.dll
```c++
extern "C" int __declspec(dllexport) value = 0;

extern "C" int __declspec(dllexport) func()
{
	return value;
}

```
---

## cstmain.exe

```c++
int main()
{
	HMODULE hDLL = LoadLibrary("cstlib.dll");
	if (hDLL == NULL)
		exit(EXIT_FAILURE);

	FARPROC pFunc = GetProcAddress( hDLL, "func");
	FARPROC pFunc1 = GetProcAddress(hDLL, "value");
	int* pValue = reinterpret_cast<int*>(pFunc1);
	*pValue = 10;
	int ret = pFunc(); //ret is 10

	FreeLibrary(hDLL);
	hDLL = NULL;
	return 0;
}
```

---
## Calling convention
+ __stdcall

  Windows API调用方式，从右向左传递参数，由**被调用方**API清理调用栈。

+ __cdecl

   C/C++ 缺省调用方式，从右向左传递参数，由**调用方**CLIENT清理调用栈，当变长参数时，只能使用这种方式。
   
   
+ __fastcall

在 __stdcall的基础上，前两个双字参数或更少的参数由寄存器来传递，更多参数还是通过寄存器
 
