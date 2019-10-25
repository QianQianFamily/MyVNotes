# typedef

## Using class
People can not foward declare a typedef.
If you using a type A as type B, in other header file, you can foward declare class B, instead you need to include A.h. Example:

**RainOpenGL.h**
```c++
#pragma once
#include <QOpenGLFunctions_4_5_Core>

namespace Rain
{
	using RainOpenGLFuncs = typename QOpenGLFunctions_4_5_Core;
}
```
**IRenderable.h**
```c++
#pragma once
namespace Rain
{
    class RainOpenGLFuncs;  //error, redifinite of  RainOpenGLFuncs.
	class IRenderable
	{
	public:
		virtual ~IRenderable() {};
		virtual void render(RainOpenGLFuncs* pContext) = 0 {};
		virtual void create(RainOpenGLFuncs* pContext) = 0 {};
		virtual void destory(RainOpenGLFuncs* pContext) = 0 {};
	};
}
```
To fix it, use #include "RainOpenGL.h" instead.
[Ref1](https://stackoverflow.com/questions/804894/forward-declaration-of-a-typedef-in-c)
[Ref2](https://stackoverflow.com/questions/14444291/why-cant-i-forward-declare-typedefs)


# Binding

```c++

typedef int Length;
extern Length val;

class Segment
{
    public:
    void setLength( Length length )  //Length is resloved as int, not float
    {
       val = length;                 //val is resolved as Segment::val, not the global::val
       std::cout << val << std::endl;
    }

    private:
    typedef float Length;
    Length  val;
}
```

Tips: 请总是吧 "nested type 声明" 放在class 起始处。