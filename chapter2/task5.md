5. 任务：猜数游戏。
 
5.1 任务简介与分析  
这个任务就是经典的猜数字游戏，游戏流程大致是：计算机在1~1000间随机选取一个数字，然后告诉玩家要在某个限定次数内将这个数字猜出来。玩家没输入一个猜测值，计算机会告诉玩家，猜大了，小了还是对了，猜中则游戏结束，失败则游戏重新开始。  
整个过程并不复杂，但既然是我们亲手做的第一个游戏，我们还是希望能把它做得有模有样，有欢迎页面，有菜单选择，有游戏说明、有GAME OVER页面，有猜中祝贺词，有游戏制作团队信息等。因此，我们把实现思路，大致步骤整理并记录下来，程序框架大概是下面这个样子：

```python
显示欢迎页面
显示游戏菜单
选择菜单玩游戏
猜数过程
显示GAME OVER
```

5.2 编程规划与伪码  
根据任务分析中的框架(甚至不用)来直接写代码完成任务也无不可，特别对前几小节中一些非常简单的任务，我们甚至都没有把程序框架描述出来。  
但其实程序规划与程序框架的形成非常重要，实际编程需要解决的的问题/任务可能会很复杂，很少能一次想清楚，**基本不能**一次编程运行成功。如果我们事先没有做清晰的程序规划，在编写了上百行或者更多的代码之后，可能会频频发现问题，然后再回头整理思考修改，如此反复，这个过程，可能会多花几倍的时间，而且可能会痛苦不堪，狼狈不堪。  
有关编程规划的相关内容可以另写一本书，我们这里只先介绍最基本的思路，即将程序流程在开始编写程序之前设计描述出来。  
**程序流程**就是我们解决问题/任务的一个个具体步骤，每一个具体步骤也可能会被分解成更具体的步骤，最后写成对应计算机代码。  
程序流程的描述要清楚明确简单，一般用**伪码**，是类似我们平时所用的语言(自然语言)和编程语言之间的一种语言，有更偏于自然语言伪码，有更偏于编程语言的伪码。上一小节中的程序框架，就是偏于自然语言的伪码。  
有了程序框架以后，我们要将其逐步细化与提炼，来继续完善程序流程设计，可以分别对每一步进行。细化过程可能需要多次，直到细化到每个步骤基本可以用程序代码简单实现。    
比如我们对`选择菜单玩游戏`进行细化： 

```python
一直等待用户选择：
    如果选择1：
        则显示游戏玩法说明
        显示游戏菜单
    如果选择2：
        则进入猜数游戏过程
    如果选择3：
        则显示GAME OVER
        退出游戏
    如果选择4：
        则显示游戏制作团队
        显示游戏菜单
```

以下是细化后的整个猜数游戏程序流程：

```python

主程序流程：

请用户输入信息
显示欢迎用户
显示游戏菜单
一直做如下步骤：
    等待用户选择
    如果选择1：
        则显示游戏玩法说明
        显示游戏菜单
    如果选择2：
        则进入猜数游戏过程
    如果选择3：
        则显示GAME OVER
        退出游戏
    如果选择4：
        则显示游戏制作团队
        显示游戏菜单

猜数函数流程：
请玩家输入一个整数n
在1-1000之间随机取一个整数number
取一个最多可猜测次数，玩家已猜测次数设为0，
一直做如下步骤直到已猜测次数大于最多可猜测次数：
    让玩家猜测一次
    玩家猜测次数加一
    告诉玩家目前猜测次数
    如果玩家猜中了：
        恭喜猜中
        显示数字及猜测次数
        退出循环
    如果玩家猜测数字大于number：
        告诉玩家猜大了
    否则：
        告诉玩家猜小了
    告诉玩家还能猜几次
否则：
    显示超过次数，猜测失败。
```

然后我们可以根据上述用伪码描述的流程来进行代码实现。

5.3 多行文本  
注意到程序流程中有显示欢迎界面，显示菜单，显示GAME OVER等，功能仅仅是显示文本，比较容易，我们先搞定这些。
首先是显示游戏菜单，由于要多次显示，因此我们将其做成函数。

```python
def menu():
    print('=====游戏菜单=====')
    print('1. 游戏说明')
    print('2. 开始游戏')
    print('3. 退出游戏')
    print('4. 制作团队')
    print('=====游戏菜单=====')

#主程序，为测试函数结果
menu()
```

`menu()`函数就是简单的一行行打印字符串，但是重复使用`print()`函数比较繁琐，python提供了用表示多行字符的表示方法，可以一并打印。
- 键入如下代码并观察执行结果。
- 
```python
def menu():
    print('''=====游戏菜单=====
                1. 游戏说明
                2. 开始游戏
                3. 退出游戏
                4. 制作团队
             =====游戏菜单=====''')
             
#主程序，为测试函数结果
menu()
```

首先我们发现，`print()`函数的两个括号之间跨越了多行。这也行？是的，python语言允许`()`内的分隔符及变量/对象之间跨越多行，还同时允许其间有空格：

```python
# ()之间跨行示例
print(100

    )

a = (5+
        10)*100

print(a)

b = 8 + (    10+
                    100)*20

def test(a,
                    b):
    print('OK')
    
test(a, 
        b)
```

但是不难看出，故意使用跨行和增加空格虽然不会报错，但是会使程序的可读性显得很差，因此要在需要的时候才使用这些方式。键入如下代码，并观察执行结果。

```python
# ()之间跨行示例2

ex_string = ('字符行1
字符行2
字符行3')
```

出现错误的原因是，整个`''`之间是一个字符串，因而不能对其跨行。

- 多行字符串表示的基本格式如下：

```python
'''
字符行1
字符行2
字符行3
  ...
字符行n
'''
```

多行字符串除了多行的特点外，其使用与一般字符串没有区别：

```python
# 多行字符串使用示例
ex_string = ''' 
            字符行1
            字符行2
            字符行3
            '''
print(ex_string)

print('''
字符行4
字符行5
字符行6''')
```

分别实现欢迎、恭喜胜利、失败及GAME OVER界面的函数(实际字符图形可由读者自行设计)：

```python
def welcome():
    print(
        '''
           ======欢迎来到猜数游戏=======
        
                     /  \     ,    ,
           _._     _ |oo| _  / \__/ \
    
          _||||   ((/ () \))   /   \
    
          |||||/|  ( ==== )    |oo|    
           \____/  _`\  /'_    /   \
    
           /   /.-' /\<>/\ `\.( () )_._      
           |    `  /  \/  \  /`'--'////)
            \__,-'`|  |.  |\/ |/\/\|"\"` 
                   |  |.  | \___/\___/  
                   |  |.  |   |    |
          
          ======欢迎来到猜数游戏=======
        '''
    )
    
def win():
    print(
        '''
           ======恭喜你，你赢了=======
        
    
                ."".    ."",
                |  |   /  /
                |  |  /  /
                |  | /  /
                |  |/  ;-._ 
                }  ` _/  / ;
                |  /` ) /  /
                | /  /_/\_/\
                |/  /      |
                (  ' \ '-  |
                 \    `.  /
                  |      |
                  |      |
          
          ======恭喜你，你赢了=======
        '''
    )
    
def lose():
    print(
        '''
           ======YOU LOSE=======
        
    
                

                   .-"      "-.
                  /            \
                 |              |
                 |,  .-.  .-.  ,|
                 | )(__/  \__)( |
                 |/     /\     \|
       (@_       (_     ^^     _)
  _     ) \_______\__|IIIIII|__/__________________________
 (_)@8@8{}<________|-\IIIIII/-|___________________________>
        )_/        \          /
       (@           `--------`
       
       
       
          ======YOU LOSE=======
        '''
    )
    
def game_over():
    print(
        '''
           ======GAME OVER=======
        
             _________ 
            / ======= \ 
           / __________\ 
          | ___________ | 
          | | -       | | 
          | |         | | 
          | |_________| |________________ 
          \=____________/                ) 
          / """"""""""" \               / 
         / ::::::::::::: \          =D-' 
        (_________________) 

       
          ======GAME OVER=======
        '''
    )
```

5.4 random模块  
现在开始实现猜数函数，得到玩家输入整数n以后，第一步是从1~n中随机取一个整数，我们似乎毫无头绪，但是不用急，这个功能只需要调用一个函数，但这次的函数调用与之前我们直接使用`input()`及`print()`内置函数略有不同，因为这个函数并非python语言内置函数，因此使用时，需要额外一步将其引入。
- 键入如下代码执行5次，并观察结果。

```python
import random

number = random.randint(1, 1000)
print(number)
```

本段代码中第一行的`import`是一个python关键字，`import`关键字的用途是加载/导入/引入**模块**。模块就是程序代码文件，可提供多个对象/函数，在被`import`进来以后，对象/函数等就可供当前程序使用。  
如果一个函数/对象就是一个模块，则模块很容易杂乱无章，于是，通常将相关功能的函数/对象组织在一起，组成一个模块。  
random模块就能够完成许多功能，提供了多个函数对象，这些函数功能都与随机数有关。比如random模块内部有一个`randint()`函数，这个函数需要两个整数参数值，然后返回这两个值之间(闭区间)的一个随机整数。
加载模块的方法就是：`import 模块名`。调用模块内函数的最常用方法是`模块名.函数名(参数表)`，可以将`.`视作`的`，即调用某模块的某个函数。  
模块加载后，自身就是一个对象，一样遵循作用域规则。键入示例并运行：

```python
# 模块加载作用域示例1

import random

def test1():
    number = random.randint(1, 1000)
    print(number)

def test2():
    num = random.randint(10, 100)
    print(num)

test1()
test2()
```

键入示例并运行：
```python
# 模块加载作用域示例2

def test():
    import random
    number = random.randint(1, 1000)
    print('test:', number)
    
test()
number = random.randint(1, 1000)    #错误，random作用域只在test()函数中
```

键入示例并运行：

```python
# 模块加载作用域示例3

def test1():
    import random
    number = random.randint(1, 1000)
    print('test1:', number)

def test2():
    number = random.randint(1, 1000)    #错误，random作用域只在test()函数中
    
test1()
test2()
```

5.5 math模块  
猜数函数流程的下一步是需要取一个最多可猜测次数，可以将这个次数设为n，基本保证99%玩家能够猜中并取得胜利。但如果想给这个游戏玩家稍微一点儿挑战，我们可将该次数设为：以2为底n的对数(具体原因请读者自行分析)。可利用在math(数学)模块中对数函数来求对数。

- 键入以下代码并观察执行结果。

```python
import math

max_times = math.log2(64)
print(max_times)
```

好，已经为游戏玩家设置了精英级的挑战难度，你是不是已经在摩拳擦掌，迫不及待了呢？让我们加快速度。

5.6 break及while...else  
首先对着函数的如下伪码，我们先一气呵成写完这个函数。

```python
猜数函数流程：
请玩家输入一个整数n
在1-1000之间随机取一个整数number
取一个最多可猜测次数，玩家已猜测次数设为0，
一直做如下步骤直到已猜测次数大于最多可猜测次数：
    让玩家猜测一次
    玩家猜测次数加一
    告诉玩家目前猜测次数
    如果玩家猜中了：
        恭喜猜中
        显示数字及猜测次数
        退出循环
    如果玩家猜测数字大于number：
        告诉玩家猜大了
    否则：
        告诉玩家猜小了
    告诉玩家还能猜几次
否则：
    显示超过次数，猜测失败。
```

 - 请键入函数代码并观察运行结果。

```python
import random, math

# 临时win(), lost()函数，测试用。
def win():
    print('Win!')
    
def lost():
    print('Lose!')
    
def guess_game():
    n = int(input('请输入一个大于0的整数，作为神秘整数的上界，回车结束。'))
    number = random.randint(1, n)
    max_times = math.ceil(math.log2(n))
    guess_times = 0
    while guess_times <= max_times:
        guess = int(input('请输入你猜测的整数，回车结束。'))
        guess_times += 1
        print('一共可以猜', max_times, '次')
        print('你已经猜了', guess_times, '次')
        
        if guess == number:
            win()
            print('神秘数字是：', guess)
            print('你比标准次数少', max_times-guess_times, '次')
            break
        elif guess > number:
            print('抱歉，你猜大了')
        else:
            print('抱歉，你猜小了')
    else:
        print('神秘数字是：', number)
        lose()

# 临时主程序，用于测试guess_game()
guess_game()
```

我们发现从根据伪码来写代码是一件较为轻松的事情，所有思路已经清楚，并记录下来，我们只要用已经掌握的python语法实现即可。  
`ceil()`是math模块中的函数，功能是由一个浮点数得到对应的向上取整的整数。  
`break`是python的关键字，用于退出`break`所在的当前层循环结构。
- 键入以下代码并观察运行结果。

```python
# break 示例

i = 0
while i < 1000:
    print('这里，i=', i)
    break

print('==================')

i = 0
while i < 1000:
    i += 1
    if i==100:
        print('if结构内部，i=', i)
        break
        
print('==================')

i = 0
j=0
while i < 5:
    print('i=', i)
    while j < 100:
        print('j=', j)
        if j == 2:
            print('break出当前层循环结构')
            break
        j += 1
    i += 1
```

关键字`else`也可以被用在while循环结构中。当while语句中的条件表达式的值成为或初始即为`False`时，运行`else`所带的语句块。此时while结构的基本形式为：

```python
while 条件表达式:       #条件表达式值为True
    循环体
else:                   #当条件表达式值为False
    语句块
```

5.7 main()函数及程序结构  
现在来看看主体流程：

```python
显示游戏菜单
一直做如下步骤：
    显示游戏菜单
    等待用户选择
    如果选择1：
        则显示游戏玩法说明
    如果选择2：
        则进入猜数游戏过程
    如果选择3：
        则显示GAME OVER
        退出游戏
    如果选择4：
        则显示游戏制作团队
```

根据主体流程伪码来实现主体流程代码，其中的玩法说明函数`show_instruction()`及游戏制作团队函数`show_team()`留给读者自行完成。

```python
# 主函数 主体流程

def main():
    while True:
        menu()
        choice = int(input('请输入你的选择')
        if choice == 1:
            show_instruction()
        elif choice == 2:
            guess_game()
        elif choice == 3:
            game_over()
            break
        else:
            show_team()


#主程序，测试 main() 用
main()
```

我们定义了一个函数，起名为main，`main()`函数中放置了整个主体流程，因此也可以称这个`main()`函数为主函数，实际上也可以起不同的名字，但是将主体流程程序起名为`main()`是编程惯例。  
将主体流程放置在`main()`函数内的好处主要有两个：
- 将主体流程所用到的对象/变量等的作用域限制在`main()`内，而不至于都成为全局变量，被其他自定义函数误用。
- 可以方便的实验不同主体流程，或者在未来将这个主体流程最终改成一个一般的函数。

一个一般的程序结构大致可规划成如下：

```python
#coding: utf-8     #指定程序代码使用的编码
'''
注释部分
'''
------------空行-----------
# 模块加载部分
import 模块1
...
import 模块2
------------空行-----------
# 用户自定义部分
def fun1()
...
def funn()
...
------------空行-----------
# 主函数部分
def main()
...
------------空行-----------
主程序部分
if __name__ = '__main__':     #后面章节会进行解释
    main()
```

5.8 拓展与知识点总结  
 - **python标准库**。`math`与`random`都是python标准库中的模块，是随着python语言的安装自动安装的。python标准库中除了一些内置函数及`math`与`random`模块外，还有很多模块，涉及到字符处理、数学计算、文件、网络、图形等等。  
python标准库的具体使用可参见官方文档：https://docs.python.org/3/library/index.html  
python标注库内容丰富功能强大，所以可以针对自己的兴趣，时常翻看python标准库的文档，了解各种库的用途。  
在实际任务中，首先要想到是否标准库中有可以实现类似功能的模块，或者是借助标准库中的模块来完成，然后查阅文档，再进行编程。  
 - `random()`函数。除了介绍过的可以用该模块下的`randint()`函数来产生随机整数以外，下例是用该模块下的`random()`直接产生[0.0, 1.0)之间的浮点数。该模块内还有很多与随机数相关的函数，具体可参考官方文档：https://docs.python.org/3/library/random.html

```python
# random生成浮点数示例
import random

i=0
while i < 5:
    n = random.random()
    print(n)
    i += 1
```

- **math**模块，提供数学函数等功能。具体函数与使用可参考官方文档：https://docs.python.org/3/library/math.html
列举几个常用的函数如下：  
`math.ceil(x)`  
Return the ceiling of x, the smallest integer greater than or equal to x.  
`math.floor(x)`  
Return the floor of x, the largest integer less than or equal to x.  
`math.exp(x)`  
Return e**x  
`math.log(x[, base])`  
With one argument, return the natural logarithm of x (to base e).  
With two arguments, return the logarithm of x to the given base.  
`math.log2(x)`  
Return the base-2 logarithm of x. This is usually more accurate than log(x, 2).  
`math.log10(x)`  
Return the base-10 logarithm of x. This is usually more accurate than log(x, 10).  
`math.sqrt(x)`  
Return the square root of x.  
`math.sin(x)`  
Return the sine of x radians.  
`math.cos(x)`  
Return the cosine of x radians.  


5.9 完整代码  

```python
'''
函数及程序结构示例
猜数游戏1.0
几个函数的具体代码，没有给出，请大家自行设计字符图案。
'''
import random, math


def win():
    #自行设计
    
def lost():
    #自行设计

def game_over():
    #自行设计

def show_team():
    #自行设计

def show_instruction():
    #自行设计

def menu():
    print('''=====游戏菜单=====
                1. 游戏说明
                2. 开始游戏
                3. 退出游戏
                4. 制作团队
             =====游戏菜单=====''')
             
def guess_game():
    n = int(input('请输入一个大于0的整数，作为神秘整数的上界，回车结束。'))
    number = random.randint(1, n)
    max_times = math.ceil(math.log(n, 2))
    guess_times = 0
    
    while guess_times <= max_times:
        guess = int(input('请输入你猜测的整数，回车结束。'))
        guess_times += 1
        print('一共可以猜', max_times, '次')
        print('你已经猜了', guess_times, '次')
        
        if guess == number:
            win()
            print('神秘数字是：', guess)
            print('你比标准次数少', max_times-guess_times, '次')
            break
        elif guess > number:
            print('抱歉，你猜大了')
        else:
            print('抱歉，你猜小了')
            
    else:
        print('神秘数字是：', number)
        lose()

# 主函数
def main():
    while True:
        menu()
        choice = int(input('请输入你的选择')
        if choice == 1:
            show_instruction()
        elif choice == 2:
            guess_game()
        elif choice == 3:
            game_over()
            break
        else:
            show_team()


#主程序
if __name__ == '__main__':
    main()
```


5.10 实践与练习  
- 练习 1：求n个随机整数均值的平方根，整数范围在m与k之间。
- 练习 2：共n个随机整数，整数范围在m与k之间，求西格玛log(随机整数)及西格玛1/log(随机整数)
- 挑战性练习：将猜数游戏改成由用户随便选择一个整数，让计算机来猜测的猜数游戏。
