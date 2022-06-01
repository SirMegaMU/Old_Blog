---
layout: post
title: 魔法属性和魔术方法
date: 2021-09-20
tags: Python
---

### `__doc__`

返回描述信息

~~~python
class Test(object):
    """这是一个类"""
    def func(self):
        """这是一个方法"""
        pass
    
test = Test()

print(Test.__doc__)
print(test.func.__doc__)
~~~

### `__module__`

返回正在操作的对象的所属模块

~~~python
from test import Test
class Test(object):
    """这是一个类"""
    def func(self):
        """这是一个方法"""
        pass
    
test = Test()

print(Test.func.__module__)

~~~



### `__class__`

返回当前操作的对象所属的类

~~~python
class Test(object):
    """这是一个类"""
    def func(self):
        """这是一个方法"""
        pass
    
test = Test()

print(Test.__class__)
~~~



### `__init__`

释放无用内存，初始化内存空间

~~~python
class Test(object):
    
    def __init__(self,args):
        self.args = args
    
    
test = Test("666")
~~~



### `__del__`

删除对象

~~~python
class Test(object):
    def func(self):
        pass

test = Test()
del test
~~~



### `__call__`

执行对象时执行此方法

~~~python
class Test(object):
    
    def __call__(self):
       
        print("666")
    
test = Test()
test()

~~~



### `__dict__`

返回类或对象的所有属性

**对象的示例属性不是对象属性！**

~~~python
class Test(object):
	string = "2333"
    def __init__(self,*args,**kwargs):
        self.args = args
        self.kwargs = kwargs
    
test = Test("666","yyds",name="test")
# 这两个不一样！
print(test.__dict__)
print(Test.__dict__)
~~~



### `__str__`

打印对象时执行此方法

~~~python
class Test(object):
    
    def __str__(self):
        return 666
    

test = Test()
print(test)
~~~



### `__getitem__`，`__setitem__`和`__delitem_`

~~~python
class Test(object):
    # 获取数据
    def __getitem__(self,key):
        print("key = ",key)
    # 设置数据
    def __setitem__(self,key,value):
        print(key," = ",value)
    删除数据
    def __delitem__(self,key):
        print("del ",key)
        
test = Test()

key1_content = test['key1'] # 执行__getitem
test['key2'] = "666" # 执行__setitem__
del test['key1'] # 执行__delitem__
~~~





