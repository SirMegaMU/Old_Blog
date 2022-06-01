---
layout: post
title: property装饰方法
date: 2021-09-19
tags: Python
---

### 基础使用

使用`@property`为类的方法做装饰  
使用`类目.被@property装饰的方法`可以直接获取该方法的返回值。

~~~python
class Test(object):
    
    def __init__(self,num):
    	self.num = num
    
    @property
    def get_num(self):
        return self.num
    
test = Test(666)
print(test.get_num)
~~~

被`@property`装饰的方法只能有`self`一个参数

### 其他使用方式

对于继承`object`的类来说可以使用`@property.setter`来使用多个参数，使用`@property.deleter`来删除属性

~~~python
class Test(object):
    
    def __init__(self,num):
        self.num = num
    
    @property.setter
    def add_arg(self,string):
        if string = "老铁666":
        	self.string = string
        
    @property.deleter
    def del_arg(self):
        pass
    
    @property
    def get_arg(self):
        return "不告诉你"
    ARG = property(get_arg)
        
test = Test(666)
# 添加属性
test.add_args = "淦啦xdm" 
# 删除属性
del test.string
# 回去属性
print(test.get_arg)
~~~

