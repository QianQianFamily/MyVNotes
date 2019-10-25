# RValue Reference

A very complete and good introduction : http://thbecker.net/articles/rvalue_references/section_01.html
yet this is another one : https://akrzemi1.wordpress.com/2011/11/09/lvalues-rvalues-and-references/

What is lvalue, rvalue, xvalue, prvalue, glvalue:
https://stackoverflow.com/questions/3601602/what-are-rvalues-lvalues-xvalues-glvalues-and-prvalues

Key things:
*  lvalues and rvalues, counter to what their names suggest, are not properties of values — they are properties of expressions. In other words, every single expression in the program is either an lvalue or an rvalue. This is a static property of the expression, that can be asserted during compilation.
* In C++11 we have two kinds of references. The one that we used to call just “reference” in C++03 is now called an lvalue reference, the other is rvalue reference.
* An lvalue reference (to non-const type) is a reference that can be initialized with an lvalue. Well, only with those lvalues that do not render const or volatile types. 
* An rvalue reference (to non-const type) is a reference that can be initialized with an rvalue (again, only with those rvalues that do not designate const or volatile types).
* An lvalue reference to const type is a reference that can be initialized with rvalues and lvalues alike (rendering constant and non-constant types).
```c++
int& a = 3; //error
const int& a = 3; // ok
int&& a = 3; //ok; you can even change a's value like a = 4 ;
```
* Any named reference (rvalue- or lvalue-) is an lvalue
*  C++11, by contrast, introduces the following reference collapsing rules1:
 A& & becomes A&
 A& && becomes A&
 A&& & becomes A&
 A&& && becomes A&&
* Rule for template deduce
template<typename T>
void foo(T&&);
Here, the following apply:
When foo is called on an lvalue of type A, then T resolves to A& and hence, by the reference collapsing rules above, the argument type effectively becomes A&.
When foo is called on an rvalue of type A, then T resolves to A, and hence the argument type becomes A&&.




