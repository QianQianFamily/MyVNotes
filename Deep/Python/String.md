# String

用关键字格式化字符串：
```python
str_template = "%(astr)s and %(anumber)f" % {'astr':'chensitan', "anumber":15 }
#print(str_template) ==> 'chensitan and 15.000000'
```
%s, %f, 等中间加（keyname）, %后跟字典

进阶用法：
```python
name = "chensitan"
age = "5"
print( "%(name)s is %(age)d" % locals() )
```