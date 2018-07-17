# 工业自动化控制－TestStand 学习笔记
## 目录
[第二章 走进TestStand](#第二章)

[第三章 TestStand系统和架构](#第三章)

[第四章 动手创建序列](#第四章)
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
