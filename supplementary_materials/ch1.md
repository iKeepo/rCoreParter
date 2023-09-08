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
