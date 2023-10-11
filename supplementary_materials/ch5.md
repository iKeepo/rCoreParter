# [第五章：进程](https://rcore-os.cn/rCore-Tutorial-Book-v3/chapter5/index.html)
## [引言](https://rcore-os.cn/rCore-Tutorial-Book-v3/chapter5/0intro.html)
之前内容的核心是通过各类演化形成了分时、虚拟化、分层、隔离等指导思想，着力点在于让程序能合理高效的运行；
到了进程，着力点成为让开发者能够控制程序的运行，所谓控制离不开交互，这就是shell的使命与到来。
“任务”是从OS执行角度的抽象，设计用户控制交互时候，需要将“任务”升级为“进程”抽象。
所谓抽象之后的对象，程序中意味着api，“进程”（进行中的程序）这个对象的基本API有create,destroy,wait,info,other。
## [进程概念及重要系统调用](https://rcore-os.cn/rCore-Tutorial-Book-v3/chapter5/1process.html)


