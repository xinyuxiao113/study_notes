python 3 中的一些注意事项：

1.不可变对象与可变对象
定义：不可变对象在修改内部的值时，id会改变(相当于重开地址新建变量)；可变对象修改内部值时，id不变.
  不可变对象：numbers, strings, tuples
  可变对象： list, dict
  

2.函数传参：
(1)不可变类型：类似 c++ 的值传递，如 整数、字符串、元组。如fun（a），传递的只是a的值，
没有影响a对象本身。比如在 fun（a）内部修改 a 的值，只是修改另一个复制的对象，不会影响 a 本身。

(2)可变类型：类似 c++ 的引用传递，如 列表，字典。如 fun（la），则是将 la 真正的传过去，修改后fun外部的la也会受影响
python 中一切都是对象，严格意义我们不能说值传递还是引用传递，我们应该说传不可变对象和传可变对象。

3.关于import:
(1)一个.py文件就是一个模块(Module), 当解释器遇到 import 语句，如果模块在当前的搜索路径就会被导入。
(2)搜索路径是一个解释器会先进行搜索的所有目录的列表.Python解释器的搜索顺序是：
    (a)当前目录
    (b)shell变量PYTHONPATH下的每个目录
    (c)默认路径,UNIX下，默认路径为 /usr/local/lib/python/
(3)一个模块只会被导入一次，不管你执行了多少次import。这样可以防止导入模块被一遍又一遍地执行。
See: https://www.runoob.com/python/python-modules.html

4.’*‘在函数赋值中的作用
https://www.cnblogs.com/lmh001/p/9960300.html
（1）打包参数
def f(*args):
  return args
*能够将所有位置参数收集形成元组 args
（2）解包参数
f(*[a,b,c])能将[a,b,c]解包成 a,b,c
f(*[a,b,c]) := f(a,b,c)
