# pointer and reference

 For pointer:
 ```c++
 int a;
const int* pA = &a;
int const* pA = &a;
```
are different.
The former one means pA can not pointer to other int value. But you can change the value of a.
The later one means you can not change the a's value by pA. But you can pointer it to another int value.

But for reference,
```c++
int a;
cosnt int& rA = a;
int const& rA = a;
```
are the same. You can not change the value a and you can not reference to other int value.
