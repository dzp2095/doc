# 工业自动化控制－TestStand 学习笔记
## 目录
[第二章 走进TestStand](#第二章)

[第三章 TestStand系统和架构](#第三章)

[第四章 动手创建序列](#第四章)

[第五章 TestStand数据空间](#第五章)

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

* 步骤内置属性 *p36  
**looping循环设置 应该合理使用:**

1.循环设置对最终操作人员不可见，导致他们不明白为什么有的步骤执行时间过长，其实是该步骤执行了很多次。  
2.在属性页面配置中设置比较隐蔽，不利于后期维护。

* 使用任意模块适配器 *p42  

合格/失败测试、数值限度测试、多数值限度测试、字符串测试、Action（动作）

* 特定模块适配器：序列调用

* 无模块适配器 *p57

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

自定义数据类型 *p89

使用容器传递数据给代码模块 *93   

* Import/Export Properties 和 Property Loader  *p102

