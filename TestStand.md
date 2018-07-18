# 工业自动化控制－TestStand 学习笔记
## 目录
[第二章 走进TestStand](#第二章)

[第三章 TestStand系统和架构](#第三章)

[第四章 动手创建序列](#第四章)

[第五章 TestStand数据空间](#第五章)

[第六章 在TestStand中调试](#第六章)

[第十二章 过程模型](#第十二章)

[第十三章 用户界面设计](#第十三章)
***
#### 第二章
* 测试和操作组织结构  
sequence file：  
main sequence + subsequence  
sequence(main or sub):setup group + main group + clean group  
Clean Group:测试发生错误时跳转至Clean Group
* TestStand组件  
TestEngine:通过API访问  
***

#### 第三章
* TestStand通用操作  
序列号追踪、流程控制、报表生成、数据存储、用户界面更新、配置和提示窗口、用户管理等

* TestStand开放式架构  
1.过程模型:通用操作+客户端序列(Main Sequence)  
2.执行入口点   
利用执行入口点定义不同的序列执行顺序    
3.回调模型    
将经常被修改的通用操作设置为回调序列，回调序列有默认可能，也可以被客户端序列文件重写
***

#### 第四章
* 创建序列 *P33 : Crtl+N

* 步骤内置属性 *p36*  
```
**looping循环设置 应该合理使用:**

1.循环设置对最终操作人员不可见，导致他们不明白为什么有的步骤执行时间过长，其实是该步骤执行了很多次。  
2.在属性页面配置中设置比较隐蔽，不利于后期维护。
```
* 使用任意模块适配器 *p42*  

合格/失败测试、数值限度测试、多数值限度测试、字符串测试、Action（动作）

* 特定模块适配器：序列调用

* 无模块适配器 *p57*

Statement、Label、Message Popup、流程控制步骤（条件、循环、Goto）、同步（用于并行测试）
***

#### 第五章
* 变量  
局部变量：同一个序列内  
Parameters参量：调用方序列->子序列  
FileGlobals文件全局变量：序列文件  
StationGlobals站全局变量：同一个计算机上的**同一个TestStand版本**的**任何**序列文件  

* 属性
Step、RunState、ThisContext(作为参数传递给代码模块或者其他序列)

* 表达式  
数据表达式、条件表达式（如先决条件：决定步骤是否被执行）、通用表达式

* 自定义数据类型  
默认数据类型：number、string、boolean、Object Reference、Container、Type(定义类型)、Array of above

Type:Error、Path、Expression等

>**注意** 应当避免在TestStand和代码模块之间传递复杂数据，尤其是二维数组和多维数组  
>**解决方法**:  
>1.DLL导出原型时尽量只包含简单数据类型  
>2.如果DLL是第三方提供的，应该先用开发环境（如VS）调用这个DLL，再封装一层，将复杂的数据类型隐藏起来。

自定义数据类型 *p89*

使用容器传递数据给代码模块 *93*   

* Import/Export Properties 和 Property Loader  *p102*
***

#### 第六章
* 调试代码模块（在代码模块的开发环境（如VS）中进行调试） *p124*

* 序列分析器  
使用内建的rules以及支撑这些rules的analysis module对处于编辑状态的序列进行分析。  
可分析的文件包括：工作区文件、序列文件、整个文件目录、自定义类型文件、站全局变量文件、代码模块以及用户文件。
***

#### 第十二章
* 执行入口点 *p240*
使得用户可以在同一过程模型中使用不同的方式执行测试

* 配置入口点 *p242*  
configure->result processing or model options  
result processing:配置哪些结果出现在报表中  

* 回调序列 *p244*  
回调序列可以在客户端序列文件中被重写

对某种特殊产品，避免了：**添加新的入口点** 或者 **创建新的过程模型**  

*引擎回调序列*:由TestStand Engine控制，数量及名称固定。**也可被重写**  
***

#### 第十三章
* TestStand UI控件*p274*
由TestStand提供的基于ActiveX的控件，分为**管理控件**和**可视化控件**。  
管理控件和可视化控件建立连接来完成显示序列、报表等功能，从而构建用户界面。  
连接完成后，可视化控件的更新就是自动的，不需要用户再干预了。  
```
管理控件:  
Application Manager Control(一个应用程序中只需要一个)  
SequenceFileView Manager Control(每个窗口中一个)  
Execution Manager Control（每处允许执行的地方需要一个）
```

* 用户界面消息UIMessage *p290*  
用于在序列文件（or过程模型）和用户界面之间传递数据，用于显示当前用户、序列执行的实时进度和状态、某变量或属性的值等。  
利用TestStand API中的*Thread.PostUIMessageEx*

用户界面数据传递至序列文件的方法：  
1.工作站全局变量  
2.在用户界面写配置文件  
3.利用UIMessage：可携带三种类型的数据，包括数值型、字符串型和ActiveX对象引用。（可将ThisContext作为ActiveX对象传递）  

