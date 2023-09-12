# [第一章：应用程序与基本执行环境](https://rcore-os.cn/rCore-Tutorial-Book-v3/chapter1/index.html)
## [引言](https://rcore-os.cn/rCore-Tutorial-Book-v3/chapter1/0intro.html)
## [应用程序执行环境与平台支持](https://rcore-os.cn/rCore-Tutorial-Book-v3/chapter1/1app-ee-platform.html)
执行环境提供服务的意思，不仅仅只是提供接口，同时意味着监控与管理；
- [strace](https://strace.io/)
strace is a diagnostic, debugging and instructional userspace utility for Linux.
It is used to monitor and tamper with interactions between processes and the Linux kernel, which include system calls, signal deliveries, and changes of process state.
- Target Triplet
cpu-manufacturer-os-runtime_library
## [移除标准库依赖](https://rcore-os.cn/rCore-Tutorial-Book-v3/chapter1/2remove-std.html)
- 编译指导属性 #[panic_handler]
用于标记核心库core中的panic!宏要对接的函数，用于让编译器把核心库core中的panic!宏定义与#[panic_handler]指向的panic函数实现合并在一起。
- lang_item start
start语义项代表了标准库std在执行应用程序之前需要进行的初始化工作；
直接删掉main函数，告诉编译器不需要初始化。
## [内核第一条指令（基础篇）](https://rcore-os.cn/rCore-Tutorial-Book-v3/chapter1/3first-instruction-in-kernel1.html)
- endianness
little-endian: 多位数的低位放在较小的地址处；endian表示内存的起始端，即低位内存；little表示数的大小；数的little部分放在内存起始点endian；
小端序、大端序，就跟进程、线程一样，如果不能准确理解，很难记清楚。
- 内存地址对齐：基本数据对齐+结构体数据对齐
CPU访问内存，通过数据总线（决定了每次读取的数据位数）+地址总线（决定了寻址范围）；
- 总线 Bus
两条总线都是直接与CPU作用，一个是寻址，一个是地址上的数据。
1. 数据总线 Data Bus
用于在计算机的不同组件之间传输数据，双向，其宽度决定了计算机系统能够同时传输的位数，更宽的data bus可以支持更高的数据传输效率和吞吐量；
2. 地址总线 Address Bus
用于传输内存或外设的地址信息，指示了CPU要读取或写入的特定内存位置或外设的位置。
决定了CPU可以寻址的数量，32位地址总线可以寻址的内存空间大小为2^32。
- 基本类型数据对齐
数据在内存中的偏移地址，必须为一个字的整数倍；
- 结构体数据对齐
结构体中的上一个数据域结束和下一个数据域开始的地方填充一些无用的字节，以保证每个数据域（基本类型数据）都能够对齐；
- 程序内存布局与编译流程
代码编译成字节形式的二进制之后可以分为代码和数据两部分。
代码是由一条条可以被CPU解码并执行的指令组成，而数据是被CPU视为可读写的内存空间。
代码和数据还可以被继续划分成段（Section）。不同的段会被编译器放置在内存不同的位置上，构成程序的内存布局（Memory Layout）。
## [内核第一条指令（实践篇）](https://rcore-os.cn/rCore-Tutorial-Book-v3/chapter1/4first-instruction-in-kernel2.html)
### 汇编
汇编是直接动作的符号化。
高级语言是动作组合的抽象。
#### 汇编语言
汇编语言的版本由两个因素限定：处理器+时间。
不同处理器有不同的指令集、寄存器和内存模型，同一类型处理器随着时间变化也会有演进。
[RISC-V手册](http://riscvbook.com/chinese/RISC-V-Reader-Chinese-v2p1.pdf)
汇编语言中不仅有处理器能够直接理解的常规指令，还有在常规基础上巧妙配置的伪指令(一种助记符)。
RISC-V手册附录A中列出了RV32/63I的所有指令、伪指令。
汇编指示符（Assemble Directives）是汇编器的命令，具有告诉汇编器代码和数据的位置、指定程序中使用的特定代码和数据常量等作用。
汇编指示符与伪指令不同，是对数据层面的操作，指令这个字符串层面，非执行层面。
## 链接
链接器有格式么，是对字节码的操作。
