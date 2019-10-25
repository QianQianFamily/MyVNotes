# operator_x

Here is a vect3 class， it also support * operator to work with float.

```c++
class vec3 {
    vec3(float x);
    vec3(float x, float y, float z);
};

tempalte<class T>
vec3 operator*(const vec3 v, const T t)
{
    return vec3(v.x*t, v.y*t, v.z*t);
}
```

Then we have following code:

```c++
float t;
vec3 v;

vec3 v1 = t*v;
```

This code has compile  strange error : no constructor for vec3( vec3, vec3, vec3).

What happen here:

1. Compile try to find operator*(float , vec3), failed.
2. Compile find operator*( vec3, vec3) defined by 12.
3. Compile find float can construct a vec3.
4. Compile instances a operator*(vec3,vec3) function and convert t to vec3.
5. For expression like v.x*t, t is type of vec3, so the return type is vec3
6. Compile didn't find vec3(vec3,vec3,vec3)

Solution 1:
1.add a new function to support it.

```c++
template<class T>
vec3 operator(const T t, const vec3 v) 
```


Solution2:
1. make vec3(float) explicit, then compile will end with no binary  function for (float , vec3).
2. don't use template ,directly use float, again compile will end with no binary  function for (float , vec3).


=====

By the way:
operator +/- can be override in two ways:

```c++

const vec3 operator-() const;
vec3 operator-(const vec3) const;

```