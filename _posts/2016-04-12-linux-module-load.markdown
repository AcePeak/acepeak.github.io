---
layout: blogs_item
title: Linux模块机制浅析
author: AcePeak
categories:
  - Internet
tags:
  - linux
  - c++
---

Linux允许用户通过插入模块，实现干预内核的目的。一直以来，对linux的模块机制都不够清晰，因此本文对内核模块的加载机制进行简单地分析。

`模块的Hello World！

我们通过创建一个简单的模块进行测试。首先是源文件main.c和Makefile。


{% highlight c++ %}
florian@florian-pc:~/module$ cat main.c
#include<linux/module.h>
#include<linux/init.h>

static int __init init(void)
{
    printk("Hi module!\n");
    return 0;
}

static void __exit exit(void)
{
    printk("Bye module!\n");
}

module_init(init);
module_exit(exit);
{% endhighlight %}


其中init为模块入口函数，在模块加载时被调用执行，exit为模块出口函数，在模块卸载被调用执行。

{% highlight bash %}
florian@florian-pc:~/module$ cat Makefile
obj-m += main.o
#generate the path
CURRENT_PATH:=$(shell pwd)
#the current kernel version number
LINUX_KERNEL:=$(shell uname -r)
#the absolute path
LINUX_KERNEL_PATH:=/usr/src/linux-headers-$(LINUX_KERNEL)
#complie object
all:
    make -C (LINUXKERNELPATH)M=(CURRENT_PATH) modules
#clean
clean:
    make -C (LINUXKERNELPATH)M=(CURRENT_PATH) clean
{% endhighlight %}

其中，obj-m指定了目标文件的名称，文件名需要和源文件名相同（扩展名除外），以便于make自动推导。

然后使用make命令编译模块，得到模块文件main.ko。

{% highlight bash %}
florian@florian-pc:~/module$ make
make -C /usr/src/linux-headers-2.6.35-22-generic M=/home/florian/module modules
make[1]: 正在进入目录 `/usr/src/linux-headers-2.6.35-22-generic'
  Building modules, stage 2.
  MODPOST 1 modules
make[1]:正在离开目录 `/usr/src/linux-headers-2.6.35-22-generic'
{% endhighlight %}

使用insmod和rmmod命令对模块进行加载和卸载操作，并使用dmesg打印内核日志。

{% highlight bash %}
florian@florian-pc:~/module$ sudo insmod main.ko;dmesg | tail -1
[31077.810049] Hi module!

florian@florian-pc:~/module$ sudo rmmod main.ko;dmesg | tail -1
[31078.960442] Bye module!
{% endhighlight %}

通过内核日志信息，可以看出模块的入口函数和出口函数都被正确调用执行。

模块文件

使用readelf命令查看一下模块文件main.ko的信息。

{% highlight bash %}
florian@florian-pc:~/module$ readelf -h main.ko
ELF Header:
  Magic:   7f 45 4c 46 01 01 01 00 00 00 00 00 00 00 00 00
  Class:                             ELF32
  Data:                              2's complement, little endian
  Version:                           1 (current)
  OS/ABI:                            UNIX - System V
  ABI Version:                       0
  Type:                              REL (Relocatable file)
  Machine:                           Intel 80386
  Version:                           0x1
  Entry point address:               0x0
  Start of program headers:          0 (bytes into file)
  Start of section headers:          1120 (bytes into file)
  Flags:                             0x0
  Size of this header:               52 (bytes)
  Size of program headers:           0 (bytes)
  Number of program headers:         0
  Size of section headers:           40 (bytes)
  Number of section headers:         19
  Section header string table index: 16
{% endhighlight %}

我们发现main.ko的文件类型为可重定位目标文件，这和一般的目标文件格式没有任何区别。我们知道，目标文件是不能直接执行的，它需要经过链接器的地址空间分配、符号解析和重定位的过程，转化为可执行文件才能执行。

那么，内核将main.ko加载后，是否对其进行了链接呢？

模块数据结构

首先，我们了解一下模块的内核数据结构。

{% highlight c++ %}
linux3.5.2/kernel/module.h:220
struct module
{
    ……
    /* Startup function. */
    int (*init)(void);
    ……
    /* Destruction function. */
    void (*exit)(void);
    ……
};
{% endhighlight %}

模块数据结构的init和exit函数指针记录了我们定义的模块入口函数和出口函数。

模块加载

模块加载由内核的系统调用init_module完成。

{% highlight c++ %}
linux3.5.2/kernel/module.c:3009
/* This is where the real work happens */
SYSCALL_DEFINE3(init_module, void __user *, umod,
       unsigned long, len, const char __user *, uargs)
{
    struct module *mod;
    int ret = 0;
    ……
    /* Do all the hard work */
    mod = load_module(umod, len, uargs);//模块加载
    ……
    /* Start the module */
    if (mod->init != NULL)
       ret = do_one_initcall(mod->init);//模块init函数调用
    ……
    return 0;
}
{% endhighlight %}

系统调用init_module由SYSCALL_DEFINE3(init_module...)实现，其中有两个关键的函数调用。load_module用于模块加载，do_one_initcall用于回调模块的init函数。

函数load_module的实现为。

{% highlight c++ %}
linux3.5.2/kernel/module.c:2864
/* Allocate and load the module: note that size of section 0 is always
   zero, and we rely on this for optional sections. */
static struct module *load_module(void __user *umod,
                unsigned long len,
                const char __user *uargs)
{
    struct load_info info = { NULL, };
    struct module *mod;
    long err;
    ……
    /* Copy in the blobs from userspace, check they are vaguely sane. */
    err = copy_and_check(&info, umod, len, uargs);//拷贝到内核
    if (err)
       return ERR_PTR(err);
    /* Figure out module layout, and allocate all the memory. */
    mod = layout_and_allocate(&info);//地址空间分配
    if (IS_ERR(mod)) {
       err = PTR_ERR(mod);
       goto free_copy;
    }
    ……
    /* Fix up syms, so that st_value is a pointer to location. */
    err = simplify_symbols(mod, &info);//符号解析
    if (err < 0)
       goto free_modinfo;
    err = apply_relocations(mod, &info);//重定位
    if (err < 0)
       goto free_modinfo;
    ……
}
{% endhighlight %}

函数load_module内有四个关键的函数调用。copy_and_check将模块从用户空间拷贝到内核空间，layout_and_allocate为模块进行地址空间分配，simplify_symbols为模块进行符号解析，apply_relocations为模块进行重定位。

由此可见，模块加载时，内核为模块文件main.ko进行了链接的过程！

至于函数do_one_initcall的实现就比较简单了。

{% highlight c++ %}
linux3.5.2/kernel/init.c:673
int __init_or_module do_one_initcall(initcall_t fn)
{
    int count = preempt_count();
    int ret;
    if (initcall_debug)
       ret = do_one_initcall_debug(fn);
    else
       ret = fn();//调用init module
    ……
    return ret;
}
{% endhighlight %}

即调用了模块的入口函数init。

模块卸载

模块卸载由内核的系统调用delete_module完成。

{% highlight c++ %}
linux3.5.2/kernel/module.c:768
SYSCALL_DEFINE2(delete_module, const char __user *, name_user,
        unsigned int, flags)
{
    struct module *mod;
    char name[MODULE_NAME_LEN];
    int ret, forced = 0;
    ……
    /* Final destruction now no one is using it. */
    if (mod->exit != NULL)
       mod->exit();//调用exit module
    ……
    free_module(mod);//卸载模块
    ……
}
{% endhighlight %}

通过回调exit完成模块的出口函数功能，最后调用free_module将模块卸载。

结论

如此看来，内核模块其实并不神秘。传统的用户程序需要编译为可执行程序才能执行，而模块程序只需要编译为目标文件的形式便可以加载到内核，有内核实现模块的链接，将之转化为可执行代码。同时，在内核加载和卸载的过程中，会通过函数回调用户定义的模块入口函数和模块出口函数，实现相应的功能。

参考资料

http://hi.baidu.com/20065562/item/15dcc4ce92c3d510b67a24af

http://blog.chinaunix.net/uid-26009923-id-3840337.html
