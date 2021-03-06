# lab0 SPOC思考题

## 个人思考题

---

能否读懂ucore中的AT&T格式的X86-32汇编语言？请列出你不理解的汇编语言。
- [x]  

>  http://www.imada.sdu.dk/Courses/DM18/Litteratur/IntelnATT.htm
基本都能读懂


虽然学过计算机原理和x86汇编（根据THU-CS的课程设置），但对ucore中涉及的哪些硬件设计或功能细节不够了解？
- [x]  

>   文件系统、虚实地址转换、互斥锁、中断、分时、内存管理


哪些困难（请分优先级）会阻碍你自主完成lab实验？
- [x]  

>   出现的问题没有得到解答，配环境太困难，不会使用git，网速太慢

如何把一个在gdb中或执行过程中出现的物理/线性地址与你写的代码源码位置对应起来？
- [x]  

>   源码是逻辑地址，页机制映射为线性地址，段机制映射为物理地址

了解函数调用栈对lab实验有何帮助？
- [x]  

>   我还不知道lab实验的具体内容。但我猜测可能对理解操作系统的完全性有帮助。

你希望从lab中学到什么知识？
- [x]  

>    文件系统、虚实地址转换、互斥锁、中断、分时、内存管理

---

## 小组讨论题

---

搭建好实验环境，请描述碰到的困难和解决的过程。
- [x]  

> 网速慢，虚拟硬盘下载不动

熟悉基本的git命令行操作命令，从github上的[ucore git repo](http://www.github.com/chyyuu/ucore_lab)下载ucore lab实验
- [x]  

> 下载完毕

尝试用qemu+gdb（or ECLIPSE-CDT）调试lab1
- [x]  

> 调试完毕

对于如下的代码段，请说明”：“后面的数字是什么含义
```
/* Gate descriptors for interrupts and traps */
struct gatedesc {
    unsigned gd_off_15_0 : 16;        // low 16 bits of offset in segment
    unsigned gd_ss : 16;            // segment selector
    unsigned gd_args : 5;            // # args, 0 for interrupt/trap gates
    unsigned gd_rsv1 : 3;            // reserved(should be zero I guess)
    unsigned gd_type : 4;            // type(STS_{TG,IG32,TG32})
    unsigned gd_s : 1;                // must be 0 (system)
    unsigned gd_dpl : 2;            // descriptor(meaning new) privilege level
    unsigned gd_p : 1;                // Present
    unsigned gd_off_31_16 : 16;        // high bits of offset in segment
};
```
- [x]  

> 这个变量占几个bit

对于如下的代码段，
```
#define SETGATE(gate, istrap, sel, off, dpl) {            \
    (gate).gd_off_15_0 = (uint32_t)(off) & 0xffff;        \
    (gate).gd_ss = (sel);                                \
    (gate).gd_args = 0;                                    \
    (gate).gd_rsv1 = 0;                                    \
    (gate).gd_type = (istrap) ? STS_TG32 : STS_IG32;    \
    (gate).gd_s = 0;                                    \
    (gate).gd_dpl = (dpl);                                \
    (gate).gd_p = 1;                                    \
    (gate).gd_off_31_16 = (uint32_t)(off) >> 16;        \
}
```
如果在其他代码段中有如下语句，
```
unsigned intr;
intr=8;
SETGATE(intr, 0,1,2,3);
```
请问执行上述指令后， intr的值是多少？
- [x]  

> 65538

请分析 [list.h](https://github.com/chyyuu/ucore_lab/blob/master/labcodes/lab2/libs/list.h)内容中大致的含义，并能include这个文件，利用其结构和功能编写一个数据结构链表操作的小C程序
- [x]  

> list.h是一个双向链表的头文件，它的每个节点都有一个前向指针和一个后向指针，其中还定义并实现了增、删、查等功能。
下面一段代码简单使用了其中的初始化和增加节点、查看节点的功能。首先构造5个节点，依次连接，最后检查尾节点的前一个是否正确。
```
#include<iostream>
#include "list.h"
using namespace std;
int main()
{
    //构造节点 
     list_entry_t* elm0=new list_entry_t;
     list_entry_t* elm1=new list_entry_t;
     list_entry_t* elm2=new list_entry_t;
     list_entry_t* elm3=new list_entry_t;
     list_entry_t* elm4=new list_entry_t;
     //构造链表 
     list_init(elm0);
     list_add(elm0, elm1);
     list_add(elm1, elm2);
     list_add(elm2, elm3);
     list_add(elm3, elm4);
     //检验结果 
     cout<<list_prev(elm4)<<' '<<elm3;
     return 0;   
}    
```
---

## 开放思考题

---

是否愿意挑战大实验（大实验内容来源于你的想法或老师列好的题目，需要与老师协商确定，需完成基本lab，但可不参加闭卷考试），如果有，可直接给老师email或课后面谈。
- [x]  

>  

---
