# constructor

``` c++

class Foo
{
    public:
    Foo()
    {
        m_data = new int[1024];
    }
    ~Foo()
    {
        if(m_data)
            delete m_data;
        m_data = nullptr;
    }
}

Foo getFoo()
{
    return Foo();
}

void main()
{
    Foo f = getFoo();
    return;
}
```

Question 1:

What will happen in line 27?
1.First Foo::Foo will be called to in line 22.
2.A copy construct will be called to copy the data to f in line 27.
3.The first Foo instance will get destroied.

Will the program crash?
Yes, when the f get destroied, it will delete the memory which had been deleted by the first instance of Foo.

How to deal with the crash?
1. Add a copy contructor to make deep copy.
2. Add a move copy constructor  and disable copy constructor to avoid deep copy and crash.

What would happen if turn on "named return value optimization"?
There will be just one Foo::Foo() contructor get called.