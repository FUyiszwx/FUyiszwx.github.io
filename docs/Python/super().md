
## super()

```
    def super(cls, inst):
        mro = inst.__class__.mro()
        return mro[mro.index(cls)+1]

```
    super相比于说是直接调用父类方法，更应该看作在mro表中寻找匹配的类。

比如
```
class A:
    def __init__(self):
        self.n = 2
    def plus(self, m):
        self.n += m
        print("{}来自A类的方法".format(self))

class B(A):
    def __init__(self):
        self.n = 3
    def plus(self, m):
        print("{}来自B类的方法".format(self))
        print(self.__class__.mro())
        super().plus(m)
        self.n += 3

class C(A):
    def __init__(self):
        self.n = 4
    def plus(self, m):
        print("{}来自C类的方法".format(self))
        print(self.__class__.mro())
        super().plus(m)
        self.n += 4

class D(B,C):
    def __init__(self):
        self.n = 5
    def plus(self, m):
        print("{}来自D类的方法".format(self))
        print(self.__class__.mro())
        super().plus(m)
        self.n += 5

d=D()
d.plus(2)
print(d.n)

输出为：
<__main__.D object at 0x0000016DE0F4BFA0>来自D类的方法
[<class '__main__.D'>, <class '__main__.B'>, <class '__main__.C'>, <class '__main__.A'>, <class 'object'>]
<__main__.D object at 0x0000016DE0F4BFA0>来自B类的方法
[<class '__main__.D'>, <class '__main__.B'>, <class '__main__.C'>, <class '__main__.A'>, <class 'object'>]
<__main__.D object at 0x0000016DE0F4BFA0>来自C类的方法
[<class '__main__.D'>, <class '__main__.B'>, <class '__main__.C'>, <class '__main__.A'>, <class 'object'>]
<__main__.D object at 0x0000016DE0F4BFA0>来自A类的方法
```

这是因为在生成D类的时候，就已经产生了D的mro表，之后的每次调用，由于传入的self都是来自D的，因此mro表没有改变，所以会在调用B类方法之后去调用C类中的方法。
