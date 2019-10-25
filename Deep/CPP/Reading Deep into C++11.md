# Reading Deep into C++11


count the number  which is less than 10 and greator than 5 in container "coll" :

```c++
std::count_if( 
    coll.begin(), coll.end(),
    std::bind( 
        std::logical_and<bool>
            (
            std::bind( std::greater<int>(), _1,5),
            std::bind( std::less<int>(),_1,10)
            )
     )
)
```

---

std::bind on class member

```c++

struct A
{
    int m_value;
}

A a;
std::function<int&(void)> func_access_A_value = std::bind( &A::m_value, &a);

func_access_A_value() = 10;
```
---

class which can be convert to function

```c++
struct Bar
{
    using func_type = void(*)(void);
    operator func_type( void )
    {
        return funcImpl;
    }
    static void funcImpl( void )
    {
        //do something
    }
}

```
---
Lambda:

1. 允许省略Lambda的返回值类型，如果编译器可以自己推断出来。
    1.1 如果返回值是初始化列表，就不能省略，返回值使用后置语法来指定。 例如 [](int a) -> int { ...}
2. 如果参数为空，允许省略参数列表。
    2.1 用mutable修饰时,不能省略参数列表。
3. 没有捕获变量的Lambda表达式可以转换成函数指针，而捕获了变量的lambda表达式则不能,（把lambda看成一个放函数对象，捕获了变量就有成员，成员函数不能转换成普通函数，因为会丢失this指针）。

capture时的细节：
 ```c++
 
 int main()
 {
     int a = 10;
    int b = 8;

   auto f = [a, b]() 
    {
        ... 
   };

   a = 11;
   b = 12;
   std::cout << f() << std::endl;
   std::cout << a << std::endl;
   std::cout << b << std::endl;
 ```
1. 在没有注明是=还是&的情况下， 默认是=捕获。
2. 用=捕获的值是Lambda声明时当前的值，不是Lambda执行时的当前值。 在执行f的时候，a还是10，b还是8.
3. 用=捕获时，在lambda内部，虽然a的类型是  int， 但仍不可以修改a的值，因为Lambda表达式的operator()默认是const的。可以理解为捕获的值是成员变量，一个const函数无法修改成员变量的值。
4. 用=捕获时，如果一定要修改，需要加上mutable关键字 : auto f = [a,b]() mutable { ... }
5. 在4的情况下，即使在Lambda内部对a进行修改，也不会影响外部的a；即使没有参数也不能省略参数列表。

如果使用&捕获，那么在：  
1. 在Lambda内部， a的值是f执行时的当前值，即11.
2. 可以修改a, 修改的同时外部的a也改了。
3. 允许这样写[=,&b] ,但是不允许[&，=b]. 后者情况下,应该写[&,b]