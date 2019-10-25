# memory_layout

1.  Alignment rules
 - 数据类型自身的对齐值：char型数据自身对齐值为1字节，short型数据为2字节，int/float型为4字节，double型为8字节。
 - 结构体或类的自身对齐值：其成员中自身对齐值最大的那个值。
  - 指定对齐值：#pragma pack (value)时的指定对齐值value。
  - 数据成员、结构体和类的有效对齐值：自身对齐值和指定对齐值中较小者，即有效对齐值=min{自身对齐值，当前指定的pack值}。
 - 结构体变量的首地址能够被其最宽基本类型成员的大小所整除；
 - 结构体每个成员相对结构体首地址的偏移量(offset)都是成员大小的整数倍，如有需要编译器会在成员之间加上填充字节(internal adding)；
 - 结构体的总大小为结构体最宽基本类型成员大小的整数倍，如有需要编译器会在最末一个成员之后加上填充字节{trailing padding}。


2.  inheritance
 - 父类在前面，自己的成员在后面， 之间可能有父类的trailing padding.
 - 如果父类有虚方法，在父类区域的开头，会插入一个虚表指针， 指向虚表。
 - 如果是多继承，每个父类会按声明顺序摆放，每个有虚方法的父类区域都会安插一个虚表指针

5. Virtual inheritance
```c++
class A;
class B: public virtual A;
class C: public virtual A;
class D: public B, public C;
```
D的内存分布：
最前面是B的区域，B的前端是一个指针，指向A的位置的偏移的大小；如果B有虚方法，还接着第二个虚表指针； 后面接B的成员。
B后面是C，C后面是D自己的数据。 D 后面是A。
B和C的开头会有1或2个指针，分别控制A的偏移和虚表。
