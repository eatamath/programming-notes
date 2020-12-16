# Architecture



##### hello.c 的执行过程

- 预处理
  - 展开宏，插入include文件，生成`.i`文件
- 编译
  - 翻译成汇编语言，`.i`文件转`.s`文件
- 汇编
  - 汇编器生成机器语言指令，并打包成可重定位目标程序（relocatable object program），结果保存在`.o`文件中（二进制文件）
- 链接
  - 调用的函数如`printf`需要合并`printf.o`文件，得到最后的`hello.o`文件（可执行文件），加载到内存中  

##### 基本硬件结构

- 总线
- IO设备
- 主存
- CPU

运行hello.c的过程见P7