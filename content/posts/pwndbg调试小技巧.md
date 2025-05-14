+++
date = '2025-05-15T00:22:07+08:00'
draft = true
title = 'Pwndbg调试小技巧'
+++
做pwn题总是离不开pwndbg等调试工具，这里记录一下一些常用的调试技巧。
<!--more-->

# 常用命令
**help查看所有命令**
---
## 调试命令
### 调试前的准备指令
- `checksec` 查看保护
- `aslr <on/off>` 开启/关闭aslr


### 控制程序的命令
- `dbg <filename>` 直接启动
- `r` 运行
- `c` 继续运行
- `n` 单步运行
- `s` 单步运行，进入函数
- `b` 设置断点
    - `b *0x7ffff7a5c060` 设置断点在地址
    - `b main` 设置断点在函数
    - `b $rebase(0xdeadbeef)` 设置断点在相对地址（常用于题目开了pie无法获得准确地址时的选择，参数就是偏移量）
    - `info b` 查看所有断点信息
    - `delete 5` 删除第5个断点
    - `disable 5` 禁用第5个断点
    - `enable 5` 启用第5个断点
    - `clear` 清除所有断点
### 查看数据内容和类型的命令
- `p` 查看变量
    - `p $esp` 查看esp寄存器
    - `p $ebp` 查看ebp寄存器
    - `p $eip` 查看eip寄存器
    - `p 10-4` 打印10-4的值
    - `p &var` 打印变量地址
    - `p *0x7ffff7a5c060` 打印地址0x7ffff7a5c060的值
    - ……（反正就是接`$寄存器名`或者表达式）
- `x` 查看内存
    - `x/10gx` 查看10个8字节内存
    - `x/10gx $esp` 查看esp寄存器指向的10个8字节内存
    - `x/10gx $rebase(0xdeadbeef)` 查看相对地址0xdeadbeef指向的10个8字节内存
    - ……（反正就是接`/个数 字节数 输出形式 内存地址`）
        - `个数` 查看多少个
        - `字节数` 查看多少字节，可以是`b`（1字节）、`h`（2字节）、`w`（4字节）、`g`（8字节）
        - 输出形式可以是`x`（16进制）、`d`（10进制）、`c`（字符）、`f`（浮点数）、`s`（字符串）、`i`（指令）
        - 内存地址可以是`$寄存器名`、`$rebase(偏移量)`、`0x地址`
- `type` 查看变量类型
    - `type var` 查看变量类型
    - `type $rebase(0xdeadbeef)` 查看相对地址0xdeadbeef的类型
- `context` 查看上下文
    - `context regs` 查看寄存器
    - `context stack` 查看寄存器、汇编、内存
- `hexdump`
    - `hexdump $rebase(0xdeadbeef)` 查看相对地址0xdeadbeef的内存
    - `hexdump $rebase(0xdeadbeef) 10` 查看相对地址0xdeadbeef的10个字节内存
- `telescope`：是比hexdump更智能的选项
    - `telescope $rebase(0xdeadbeef)` 查看相对地址0xdeadbeef的内存
- `vmmap` 查看内存映射
- `disassemble` 查看汇编
    - `disassemble main` 查看main函数的汇编
    - `disassemble $rebase(0xdeadbeef)` 查看相对地址0xdeadbeef的汇编
- `search` 查看内存中是否有某个值
- `rop` 查看rop链
- `plt` 查看plt表
- `got` 查看got表
- `symbols` 查看符号表
- `info` 查看信息
    - `info registers` 查看寄存器
    - `info args` 查看函数参数
    - `info locals` 查看局部变量
    - `info breakpoints` 查看断点
    - `info functions` 查看函数
    - `info variables` 查看变量
    - `info files` 查看文件
    - `info threads` 查看线程
- `dps` 优雅地输出内容
    - `dps $esp` 优雅地输出esp寄存器指向的内存
    - `dps $rebase(0xdeadbeef)` 优雅的输出相对地址0xdeadbeef指向的内存
    - `dps addr` 优雅地输出地址指定地址的内存
- `procinfo` 查看进程信息
- `canary` 查看canary
- `stack` 查看栈
    - `stack 10` 查看栈顶10个元素
    - `retaddr` 查看所有的返回地址
### 堆相关命令
- `heap` 查看堆
    - `heap -v` 查看堆详细信息
    - `heap -s` 查看堆简略信息
    - `heap addr` 查看指定地址的堆以及高地址堆
    - `heapbase` 查看堆基地址
    - `heapinfo` 查看堆信息
    - `heapinfoall` 查看所有堆信息(我的评价是不如bins)
    - `parseheap` 优雅地显示堆
- `arena` 显示arena的基本信息
    - `arenas` 显示所有arena的基本信息
    - `arenainfo` 优雅地显示arena的基本信息
- `bins` 查看所有种类的堆块的链表信息
    - `fastbins` 显示fastbins的链表信息
    - `largebins` 显示largebins的链表信息
    - `smallbins` 显示smallbins的链表信息
    - `unsortedbins` 显示unsortedbins的链表信息
    - `tcachebins` 显示tcachebins的链表信息
        - `tcache` 显示tcache的详细信息
- `tracemalloc` 跟踪堆分配(没成功，不知道怎么用)

### 格式化字符串漏洞相关命令
- `cyclc` 有规律地生成一串字符串
    - `cycle 10` 生成10个字符的字符串
    - `cycle -l "aaag"` 由于cyclic是生成有规律的一串字符串，所以在应对格式化字符串的时候，如果不知道格式化字符串的长度，可以先使用`cyclic 100`生成一大串字符串，输入进去，然后直接c，程序就会报错，返回对应的地址被覆盖了，假如被覆盖成“aaag”，就可以使用`cycle -l “aaag”`来快速获取偏移，注：此时输出的偏移对应着ret对应的地方。


