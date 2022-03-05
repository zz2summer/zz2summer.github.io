# 软件工程基础 实验4《系统实现》


本文内容主要是讲解软件工程基础中实验四，根据课程管理对象类图，采用Java在Eclipse下编码实现，并用JUnit框架对某Java类进行测试。针对某网站，采用selenium或SilkTest或SilkPerformer分别进行功能测试和性能测试。（选做）

<!--more-->

> 版权声明：本文为博主原创文章，遵循 [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) 版权协议，禁止商用，转载请附上原文出处链接和本声明。

#### 实验4《系统实现》

##### 一、实验目的
1. 掌握：系统实现的有关技术及其相关工具。

##### 二、实验内容
1. 试对图3所示的课程管理对象类图，采用Java在Eclipse下编码实现，并用JUnit框架对某Java类进行测试。

  ![在这里插入图片描述](https://raw.githubusercontent.com/summer2zz/pictures/master/blogs/20210411083314.png)


<center>图3  类图</center>

2. 针对某网站，采用selenium或SilkTest或SilkPerformer分别进行功能测试和性能测试。（选做）

##### 三、实验方法
1. 利用pycharm工具，python代码实现该课程管理系统；
2. 利用python中的doctest和unittest等测试工具对系统中的代码进行测试。

##### 四、实验步骤
&emsp;&emsp;**4.1 需求说明： 课程管理系统**

&emsp;&emsp;A、管理员：

&emsp;&emsp;创建老师：姓名、性别、年龄、资产

&emsp;&emsp;创建课程：课程名称、上课时间、课时费、关联老师

使用pickle保存在文件

&emsp;&emsp;B、学生：

&emsp;&emsp;学生：用户名、密码、性别、年龄、选课列表[]、上课记录

&emsp;&emsp;1、列举所有课程

&emsp;&emsp;2、选择课程

&emsp;&emsp;3、学生上课，

&emsp;&emsp;4、ret = 课程.work() 获取课程的返回; 资产+=课时费

&emsp;&emsp;**4.2 代码思路**

&emsp;&emsp;1.类的关联：

&emsp;&emsp;a、Teacher类：关联管理员，由哪个管理员创建

&emsp;&emsp;b、 Course类：关联老师对象、管理员对象（注意：关&emsp;&emsp;联的是对象）

&emsp;&emsp;2.文件的写入：

&emsp;&emsp;a、管理员文件：写入的是管理员对象（封装管理员的用户名和密码）

&emsp;&emsp;b、学生文件：写入的是学生对象（封装了学生已选课程列表，已经上过的课程字典：key：课程对象 value：上课信息列表，是列表格式）

&emsp;&emsp;c、课程列表course_list、老师列表teacher_lis，都是列表格式。 

&emsp;&emsp;**4.3 文件概述**

&emsp;&emsp;bin目录：存放administrator.py文件和students.py文件

&emsp;&emsp;config目录：存放settings.py文件，即配置文件

&emsp;&emsp;db目录：存放与数据相关的文件，包括课程列表course_list、老师列表teacher_list、学生文件夹、管理员文件夹

&emsp;&emsp;lib目录：存放models.py文件，即存放公共的模块

&emsp;&emsp;log目录：存放日志文件

&emsp;&emsp;**4.4 代码实现**

&emsp;&emsp;**4.5 代码测试**

##### 五、实验结果
&emsp;&emsp;**5.1 利用doctest测试students.py中的登录模块**
```python
def login(user, pwd):
    """
    >>> login("","")
    用户账号或者密码输入为空
    >>> login("a","1")
    账号或者密码错误
    >>> login("a","123")
    登录成功
    """
    if ("".__eq__(user) | "".__eq__(pwd)):
        print('用户账号或者密码输入为空')
    else:
        if ("a".__eq__(user) & "123".__eq__(pwd) ):  # 如果登陆成功
            print("登录成功")
        else:
            print('账号或者密码错误')


if __name__ == '__main__':
    import doctest
    doctest.testmod(verbose=True)
```
&emsp;&emsp;**测试结果：**

![在这里插入图片描述](https://raw.githubusercontent.com/summer2zz/pictures/master/blogs/20210411083326.png)

![在这里插入图片描述](https://raw.githubusercontent.com/summer2zz/pictures/master/blogs/20210411083333.png)

&emsp;&emsp;结果分析：测试结果显示三个测试均成功通过，在用户登录时该模块能够对用户的输入进行正常判断，比如判空、账号密码核实。

&emsp;&emsp;**5.2 利用unittest测试modules.py文件中的老师类Teacher**
&emsp;&emsp;**teacher.py：**
```python
import time

class Teacher:
    """
    封装老师的相关信息
    """
    def __init__(self, name, age, admin):
        self.name = name
        self.age = age
        self.__assets = 0
        self.create_time = time.strftime('%Y-%m-%d %H:%M:%S')
        self.create_admin = admin

    def gain(self, cost):
        """
        增加资产
        :param cost: 增加的数量
        :return:
        """
        self.__assets += cost
        return self.__assets

    def decrease(self, cost):
        """
        减少资产
        :param cost: 减少的数量
        :return:
        """
        self.__assets -= cost
        return self.__assets
```
&emsp;&emsp;**unittestTeacher.py：**
```python
import unittest
from teacher import *

class Test_teacher(unittest.TestCase):
    def setUp(self):
        print('test kick on')
        self.obj = Teacher("张三",35,"胡主任")

    def test_gain(self):
        self.assertEqual(15,self.obj.gain(15))
        print('test gain')

    def test_decrease(self):
        self.assertEqual(10,self.obj.decrease(5))
        print('test decrease')

    def tearDown(self):
        print('test is over')

if __name__=='__main__':
    unittest.main()
```
&emsp;&emsp;**测试结果：**

![在这里插入图片描述](https://raw.githubusercontent.com/summer2zz/pictures/master/blogs/20210411083346.png)

&emsp;&emsp;结果分析：根据结果显示，其中测试中两个通过，一个失败，在用户创建老师类时能够成功创建，增加资产时以初始态0为基础，所以加上15等于15，测试通过，但是减少资产时依旧以0为基础，所以此处减少后为-5，而不等于10，测试未通过。

##### 六、实验结论
&emsp;&emsp;本次实验测试是进行抽样测试，根据不同的测试方式进行不同测试，测试样例、结果和结果分析见第五点显示，通过该实例测试方式可对本程序其余模块进行测试，从而验证所以模块的正确性。

&emsp;&emsp;根据本次测试结果，可知，对python进行不同方式的测试很有必要，因为测试是提高代码质量和可维护性的一种方式，也是成本最低的一种方式，尽早排除尽可能出现的bug，可以减少在后续阶段解决bug的成本（包括时间成本、人力成本等）。

&emsp;&emsp;项目源码展示如下：

&emsp;&emsp;6.1 配置文件settings.py

```python
import os
BASE_DIR = os.path.dirname(os.path.dirname(__file__))  #配置文件的上级目录
BASE_ADMIN_DIR = os.path.join(BASE_DIR, "db", "admin")  #管理员目录
BASE_STUDENTS_DIR = os.path.join(BASE_DIR, "db", "students")  #学生目录
TEACHER_DB_DIR = os.path.join(BASE_DIR, "db", "teacher_list") #老师列表目录
COURSE_DB_DIR = os.path.join(BASE_DIR, "db", "course_list")  #课程列表目录
````
&emsp;&emsp;6.2 公共模块modules.py
```python
#!/usr/bin/env python
# -*- coding:utf-8 -*-
import random
import time
import pickle
from config import settings
import os
class Teacher:
    """
    封装老师的相关信息
    """
    def __init__(self, name, age, admin):
        self.name = name
        self.age = age
        self.__assets = 0
        self.create_time = time.strftime('%Y-%m-%d %H:%M:%S')
        self.create_admin = admin
 
    def gain(self, cost):
        """
        增加资产
        :param cost: 增加的数量
        :return:
        """
        self.__assets += cost
 
    def decrease(self, cost):
        """
        减少资产
        :param cost: 减少的数量
        :return:
        """
        self.__assets -= cost
 
class Course:
    """
    课程相关信息
    """
    def __init__(self, course_name, cost, teacher_obj, admin):
        self.course_name = course_name
        self.cost = cost
        self.teacher = teacher_obj
        self.create_time = time.strftime('%Y-%m-%d %H:%M:%S')
        self.create_admin = admin
 
    def have_lesson(self):
        """
        课程上课，自动给相关联的任课老师增加课时费
        :return: 课程内容返回给上课者
        """
        self.teacher.gain(self.cost)
 
        content = random.randrange(10, 100)
        r = time.strftime('%Y-%m-%d %H:%M:%S')
        temp = "课程：%s；老师：%s；内容：%d；时间：%f" % (self.course_name, self.teacher, content, r)
        return temp
 
    def absence(self):
        """
        教学事故
        :return:
        """
        self.teacher.decrease(self.cost * 2)
 
class Admin:
    def __init__(self):
        self.username = None
        self.password = None
 
    def login(self, user, pwd):
        """
        管理员登陆
        :param user:
        :param pwd:
        :return:
        """
        if self.username == user and self.password == pwd:
            return True
        else:
            return False
 
    def register(self, user, pwd):
        """
        管理员注册
        :param user:
        :param pwd:
        :return:
        """
        self.username = user
        self.password = pwd
 
        path = os.path.join(settings.BASE_ADMIN_DIR, self.username) #管理员目录
        pickle.dump(self, open(path, 'xb'))     #将管理员对象写入文件
 
 
class Student:
    """
    学生相关信息
    """
    def __init__(self):
        self.username = None
        self.password = None
 
        self.course_list = []
        self.study_dict = {}
 
    def select_course(self, course_obj):
        """
        学生选课
        :param course_obj:
        :return:
        """
        self.course_list.append(course_obj) #将课程对象添加进课程列表
 
    def study(self, course_obj):
        """
        学生上课
        :param course_obj:
        :return:
        """
        class_result = course_obj.have_lesson()  #获取学生上课信息
 
        if course_obj in self.study_dict.keys():  #key：课程对象 value：上课信息列表，是列表格式
 
            self.study_dict[course_obj].append(class_result)  #将上课信息列表添加进上一次的列表中
        else:
            self.study_dict[course_obj] = [class_result, ]   #创建该课程对象的键值对
 
    def login(self, user, pwd):
        """
        学生登陆
        :param user:
        :param pwd:
        :return:
        """
        if self.username == user and self.password == pwd:
            return True
        else:
            return False
 
    def register(self, user, pwd):
        """
        学生注册
        :param user:
        :param pwd:
        :return:
        """
        self.username = user
        self.password = pwd
 
        path = os.path.join(settings.BASE_STUDENTS_DIR, self.username)  #学生目录
        pickle.dump(self, open(path, 'xb')) #将学生对象写入学生目录
```

&emsp;&emsp;6.3 管理员文件administrator.py
```python
#!/usr/bin/env python
# -*- coding:utf-8 -*-
import os
import sys
sys.path.append(os.path.dirname(os.path.dirname(__file__)))
 
import random
import time
import pickle
import os
from lib import models
from config import settings
from lib.models import *
 
def create_course(admin_obj):
    teacher_list = pickle.load(open(settings.TEACHER_DB_DIR, 'rb'))  #读取老师清单
    for num, item in enumerate(teacher_list, 1):                     #打印老师清单
        print(num, item.name,item.age,item.create_time,item.create_admin.username)
    course_list = []    #创建课程列表
    while True:
        name = input('请输入课程名称(q退出)：')
        if name == 'q':
            break
        cost = input('请输入课时费：')
        num = input('选择老师(序号)：')
        obj = models.Course(name, cost, teacher_list[int(num)-1], admin_obj)  #创建课程对象
        course_list.append(obj)
 
    if os.path.exists(settings.COURSE_DB_DIR):  #如果有课程列表
        exists_list = pickle.load(open(settings.COURSE_DB_DIR, 'rb'))
        course_list.extend(exists_list)         #对原有课程列表进行扩展
    pickle.dump(course_list, open(settings.COURSE_DB_DIR, 'wb'))   #将学生列表写入文件
 
def create_teacher(admin_obj):
    teacher_list = []       #创建老师列表
    while True:
        teacher_name = input('请输入老师姓名(q表示退出)')
        if teacher_name == 'q':
            break
        teacher_age = input('请输入老师年龄')
        obj = models.Teacher(teacher_name, teacher_age, admin_obj)  #创建老师对象
        teacher_list.append(obj)
    if os.path.exists(settings.TEACHER_DB_DIR):
        exists_list = pickle.load(open(settings.TEACHER_DB_DIR, 'rb'))
        teacher_list.extend(exists_list)   #对原有老师列表进行扩展
    pickle.dump(teacher_list, open(settings.TEACHER_DB_DIR, 'wb'))  #将老师列表写入文件
 
def login(user,pwd):
    if os.path.exists(os.path.join(settings.BASE_ADMIN_DIR, user)):
        # 从文件中将管理员对象读取出来（里面封装了用户信息以及提供了登录方法）
        admin_obj = pickle.load(open(os.path.join(settings.BASE_ADMIN_DIR, user), 'rb'))
        if admin_obj.login(user, pwd):
            print('登录成功')
            while True:
                sel = input("1、创建老师；2、创建课程")
                if sel == '1':
                    create_teacher(admin_obj)
                elif sel == '2':
                    create_course(admin_obj)
                else:
                    break
 
        else:
            return 1
    else:
        return 0
 
def regiter(user,pwd):
    admin_obj = models.Admin()
    admin_obj.register(user, pwd)
 
 
def main():
    inp = input("1、管理员登录；2、管理员注册；\n >>>")
    user = input('请输入用户名:')
    pwd = input('请输入密码:')
 
    if inp == '1':
        ret = login(user, pwd)
        if ret == 1:
            print('密码错误')
        elif ret == 0:
            print('用户不存在')
 
    elif inp == '2':
        regiter(user, pwd)
 
 
if __name__ == "__main__":
    main()
```
&emsp;&emsp;6.4 学生文件students.py
```python
#!/usr/bin/env python
# -*- coding:utf-8 -*-
import os
import sys
sys.path.append(os.path.dirname(os.path.dirname(__file__)))
import pickle
from lib import models 
from config import settings
from lib.models import  Course
from lib.models import  Admin
from lib.models import  Teacher
 
 
def course_info(student_obj):   #打印已选课程信息
    for item in student_obj.course_list:
        print(item.course_name, item.teacher.name)
 
 
def select_course(student_obj):  #选择课程
    course_list = pickle.load(open(settings.COURSE_DB_DIR, 'rb'))  #从文件读取课程
    for num, item in enumerate(course_list, 1):
        print(num, item.course_name, item.cost, item.teacher.name)  #打印课程列表
    while True:
        num = input("请选择课程(q退出):")
        if num == "q":
            break;
        selected_course_obj = course_list[int(num)-1] #根据序号选择课程
        if selected_course_obj not in student_obj.course_list:
            student_obj.course_list.append(selected_course_obj) #添加进该学生的课程列表
    pickle.dump(student_obj, open(os.path.join(settings.BASE_STUDENTS_DIR, student_obj.username), 'wb'))#将学生对象dump进文件，封装学生选课列表，上课字典信息
 
def login(user, pwd):
    if os.path.exists(os.path.join(settings.BASE_STUDENTS_DIR, user)):
        student_obj = pickle.load(open(os.path.join(settings.BASE_STUDENTS_DIR, user), 'rb'))
        if student_obj.login(user,pwd):  #如果登陆成功
            while True:
                inp = input('1、选课；2、上课；3、查看课程信息')
                if inp == '1':
                    select_course(student_obj)
                elif inp == '3':
                    course_info(student_obj)
                else:
                    break
        else:
            print('密码错误')
    else:
        print('用户不存在')
 
 
def register(user, pwd):
    obj = models.Student()
    obj.register(user,pwd)
 
 
def main():
    inp = input('1、登录；2、注册 \n >>>')
    user = input("用户名：")
    pwd = input("密码：")
    if inp == "1":
        login(user,pwd)
    elif inp == "2":
        register(user, pwd)
 
 
if __name__ == "__main__":
    main()
```
##### 七、实验小结
&emsp;&emsp;通过本次实验主要是学会了利用python的相关技术对代码进行测试，有doctest、unittest等等，利用这些测试可以极大的优化代码与减少后期的开发成本。

&emsp;&emsp;实验时最开始遇到的问题是对于实验内容中给出的UML图不知如何进行代码实现，毫无头绪，后来是在独立思考一段时间后以及与同学互相讨论从而进行实验开展。

&emsp;&emsp;在实验过程中遇到了低级错误，就是进行unittest单元测试时重新写了一个py文件进行测试，然而当时为了明确该文件作用就直接命名为了unittest，在写代码时就一直报错显示unittest没有TestCase等参数，一直运行不了，后来通过百度搜索得知该错误，将文件名更改即解决了。

&emsp;&emsp;实验中有待改进的地方主要是该项目的代码有待优化，测试样例可以进一步增加。



参考文章：

【1】[软件工程基础实验 - 百度文库](https://wenku.baidu.com/view/e96d3a66f8c75fbfc77db2ff.html)

【2】[Python作业-选课系统 - ygqygq2 - 博客园](https://www.cnblogs.com/ygqygq2/p/6727697.html)

【3】[python实现学生选课系统 面向对象的应用： - wangheng1409 - 博客园](https://www.cnblogs.com/wanghzh/p/5560787.html)
