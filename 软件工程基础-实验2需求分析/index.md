# 软件工程基础 实验2《需求分析》


本文内容主要是讲解软件工程试验三——某培训中心要研制一个计算机管理系统，根据描述中找出绘制数据流图的四种成分并用Visio绘制数据流图。有一简单选课系统，用文字描述如下，试用IDEF1X图和UML类图描述该系统的信息模型，并用Visio或EA绘制该IDEF1X图和UML类图。请用Visio或EA绘制如图2所示的用例图。

<!--more-->

> 版权声明：本文为博主原创文章，遵循 [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) 版权协议，禁止商用，转载请附上原文出处链接和本声明。

#### 实验2《需求分析》

##### 一、实验目的

1. 了解：软件项目需求分析的基本原理与方法；
2. 掌握：用例建模方法、数据流建模方法和IDEF1X数据建模方法；
3. 掌握：Visio/EA等工具绘制模型图。

##### 二、实验内容

&emsp;&emsp;1、请从下面的描述中找出绘制数据流图的四种成分并用Visio绘制数据流图。

&emsp;&emsp;某培训中心要研制一个计算机管理系统。它的业务是：将学员发来的信件收集分类后，按几种不同的情况处理。

&emsp;&emsp;（1) 如果是报名的，则将报名数据送给负责报名事务的职员，他们将查阅课程文件，检查该课程是否额满，然后在学生文件、课程文件上登记，并开出报告单交财务部门，财务人员开出发票给学生。

&emsp;&emsp;（2) 如果是想注销原来已选修的课程，则由注销人员在课程文件、学生文件和帐目文件上做相应的修改，并给学生注销单。

&emsp;&emsp;（3）如果是付款的，则由财务人员在帐目文件上登记，也给学生一张收费收据。

&emsp;&emsp;2、 有一简单选课系统，用文字描述如下，试用IDEF1X图和UML类图描述该系统的信息模型，并用Visio或EA绘制该IDEF1X图和UML类图。

&emsp;&emsp;1）**基本描述**：在该系统中，有学院、教师、课程、学生等实体，他们的属性分别是：

&emsp;&emsp;学院：学院编号、学院名称、地址、联系电话、院长等基本属性；

&emsp;&emsp;教师：教师编号、姓名、性别、年龄、职称、所在学院等属性；

&emsp;&emsp;课程：课程编号、课程名称、课程性质（必修/选修）、学分、开课学院等属性；

&emsp;&emsp;学生：学号、姓名、性别、年龄、入学时间、学院等属性。

&emsp;&emsp;教学班实体：教学班号、上课教师、课程、上课学期、上课时间、上课周次。

&emsp;&emsp;2）**功能需求如下**：

&emsp;&emsp;（1）能完成基本信息的维护：即各实体的基本信息的增、删、改、查。

&emsp;&emsp;（2）排课：为教师安排一学期所上的课程。一位教师在一学期可以上一门课或多门课，也可以不上课；一门课可以有多个教师上，但是不同的教师上的课应该属于不同的教学班。

&emsp;&emsp;（3）学生选课：学生根据教学要求进行选课。在学生选课之前检查该学生是否有选课资格（比如是否欠费、前期课程是否修完并通过）；一个学生可以选多门课、一门课可以被多个学生选修，但是一个学生不能选择同一门课的不同教学班；如果学生选了一门课的某个教学班后再选该门课的其他教学班系统应做出出错提示；统计已选教学班的学生人数；一个教学班的选课名额有限；学生选课后，如果发现选课不合理可以退选、重选；选课结束后应提供打印课程表的功能。

&emsp;&emsp;3、请用Visio或EA绘制如图2所示的用例图。

![在这里插入图片描述](https://raw.githubusercontent.com/summer2zz/pictures/master/blogs/20210411082807.png)

<center>图2 用例图</center>

##### 三、实验方法

&emsp;&emsp;运用Visio2010工具进行数据流图、UML图和IDEF1X图设计。

##### 四、实验步骤

&emsp;&emsp;1．打开Visio2010工具，选择【文件】→【新建】→【数据流】→【数据流图表】→【创建】，即可创建一个数据流图模板，之后在左侧即可选择适当图形进行数据流图绘制；

![在这里插入图片描述](https://raw.githubusercontent.com/summer2zz/pictures/master/blogs/20210411082815.png)

![在这里插入图片描述](https://raw.githubusercontent.com/summer2zz/pictures/master/blogs/20210411082822.png)

![在这里插入图片描述](https://raw.githubusercontent.com/summer2zz/pictures/master/blogs/20210411082827.png)

![在这里插入图片描述](https://raw.githubusercontent.com/summer2zz/pictures/master/blogs/20210411082841.png)

&emsp;&emsp;2．根据实验1要求，绘制数据流图，先按照各成分绘制，之后再将相关部分进行联系，并调整整体展示效果；

&emsp;&emsp;3．新建UML类图，按要求完成实验2-1；

&emsp;&emsp;4．新建IDEF1X图，按要求完成实验2-2；

&emsp;&emsp;5．新建用例图，按要求完成实验3。

##### 五、实验结果

&emsp;&emsp;1．实验1数据流图如下所示：

![在这里插入图片描述](https://raw.githubusercontent.com/summer2zz/pictures/master/blogs/20210411082859.png)

&emsp;&emsp;2．实验2的UML图如下所示：

![在这里插入图片描述](https://raw.githubusercontent.com/summer2zz/pictures/master/blogs/20210411082906.png)

![在这里插入图片描述](https://raw.githubusercontent.com/summer2zz/pictures/master/blogs/20210411082926.png)



![在这里插入图片描述](https://raw.githubusercontent.com/summer2zz/pictures/master/blogs/20210411082938.png)

&emsp;&emsp;3．实验2的IDEF1X图如下所示：

![在这里插入图片描述](https://raw.githubusercontent.com/summer2zz/pictures/master/blogs/20210411082953.png)

&emsp;&emsp;4．实验3的用例图如下所示：



![在这里插入图片描述](https://raw.githubusercontent.com/summer2zz/pictures/master/blogs/20210411083007.png)

![在这里插入图片描述](https://raw.githubusercontent.com/summer2zz/pictures/master/blogs/20210411083021.png)

![在这里插入图片描述](https://raw.githubusercontent.com/summer2zz/pictures/master/blogs/20210411083116.png)

![在这里插入图片描述](https://raw.githubusercontent.com/summer2zz/pictures/master/blogs/20210411082402.png)

&emsp;&emsp;采购人员可以登录系统、形成订单、取消订单、填写订单、检查报价、提交需求表；

&emsp;&emsp;顾客可以形成订单；

&emsp;&emsp;部门主管可以签写报表；

&emsp;&emsp;财务人员可以查询财务数据、检查基本价格表、核实预售表、核实预售单；

&emsp;&emsp;开单员可以把自己所能查看到的信息打印出来，比如单据和提货单；

&emsp;&emsp;仓库员维护着整个仓库的入库出库状况，负责开出库单，审核入库单，打印导出数据等功能；

&emsp;&emsp;物流员可以把自己所能查看到的信息打印出来，比如加工单、运输单、入库单等；


##### 六、实验结论

&emsp;&emsp;本次实验主要是对项目进行需求分析建模，有数据流图、UML图和IDEF1X图等，通过一系列建模从而对需求更加了解，也更加有利于项目计划开展。

&emsp;&emsp;实验结果的截图和文字分析见第五点。

##### 七、实验小结

&emsp;&emsp;通过本次实验主要学会了绘制一些项目中常见的模型，比如数据流图、UML图、IDEF1X和用例图等，通过模型进而对需求进行抽象，得到自己所关心得部分，从而有利于项目的开发进行。

&emsp;&emsp;实验中遇到的主要问题是模型绘制的注意事项不是很了解，比如IDEF1X的实体如何分类、如何定义实体间的联系等，解决方式主要是通过对书本的反复阅读以及案例分析，其次就是一部分关系无法确定如何将在模型中展示，这个主要是与同学交流解决。

&emsp;&emsp;待改进的主要是实验2中有部分要求无法在规定的模型中展示，后续考虑通过其他模型进行展示，还有就是用例图中关系没有充分的完全展示出来，有待进一步优化。


