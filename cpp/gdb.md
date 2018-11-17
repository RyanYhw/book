# GDB

## core dump

<pre>
gcore pid // 生成core文件, 程序不必退出
</pre>

## 其他

### 调试多进程

<pre>
set follow-fork-mode [parent|child]

parent: fork之后继续调试父进程，子进程不受影响。
child: fork之后调试子进程，父进程不受影响。
</pre>


[使用 GDB 调试多进程程序](http://www.ibm.com/developerworks/cn/linux/l-cn-gdbmp/)

### attach 进程

``` gdb attach pid ```

### 线程信息

```
info threads  # 查看线程：使用可以查看运行的线程。
thread ${num} # 切换线程
```


## 汇编
1. gcc -S -masm=intel test.c 生成intel风格的汇编文件
2. gdb 中set disassembly-flavor intel 可以显示intel风格的汇编
3. gdb 中disassemble可以显示汇编，如
<pre>
这段代码有问题，可以忽略
   0x00000000004004f0 <+0>:	mov    eax,0x2000
   0x00000000004004f5 <+5>:	mov    ss,eax
   0x00000000004004f7 <+7>:	mov    sp,0x0
   0x00000000004004fb <+11>:	add    sp,0xa
   0x00000000004004ff <+15>:	pop    ax
   0x0000000000400501 <+17>:	pop    bx
   0x0000000000400503 <+19>:	push   ax
   0x0000000000400505 <+21>:	push   bx
   0x0000000000400507 <+23>:	pop    ax
   0x0000000000400509 <+25>:	pop    bx
   0x000000000040050b <+27>:	mov    ebx,0x0
   0x0000000000400510 <+32>:	mov    eax,0x1
   0x0000000000400515 <+37>:	int    0x80
   0x0000000000400517 <+39>:	nop    WORD PTR [rax+rax*1+0x0]

</pre>  
想在0x00000000004004ff加断点, b *0x00000000004004ff 即可  

4. info registers 显示所有寄存器的值
5. p/x xxxx 可以按照16进制打印变量
6. p/x $ax 打印ax寄存器的值
7. 多进程情况下的调试set follow-fork-mode [parent|child]
