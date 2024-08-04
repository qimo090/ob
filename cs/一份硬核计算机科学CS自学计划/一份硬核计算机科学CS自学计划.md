[[推荐] 波波: 一份硬核计算机科学CS自学计划 · 语雀](https://www.yuque.com/ob26eq/cv94p5/xi9hwb)

[C语言基础](https://www.notion.so/30456c277c624482aff164401e8f5e2b?pvs=21)

# CS 学习计划

## 先导课（三个月）

课程：C语言基础
参考课程：[[2014 SP]MSU: CSE 251 Programming in C](https://www.yuque.com/ob26eq/nshoar/bhhebg)
参考书：The Absolute Beginner's Guide to C (或其它C语言参考书)
参考视频：B站上有很多不错的C语言教程，自己找
挑战难度：3星
产出目标：完成课程站点上的所有 14 个Steps实验 + 3 个 Projects
说明：
- 这门课相当于是CS101，为什么要学C语言？因为C语言是现在主流语言的鼻祖，也是主流系统编程语言，系统架构师必须懂C语言。另外，下门课程[深入理解计算机系统]需要C语言+Linux编程基础。
- 课程站点上面的PPT可以大致浏览一下，如果已经有足够编程基础的话，书可看可不看，关键是14个实验和3个项目要搞定。

## 第1年上半年

课程：深入理解计算机系统
参考课程：[[2017] Washington: CSE351 The Hardware Software Interface](https://www.yuque.com/ob26eq/nshoar/eceu3c)
参考书籍：[[教材] [CSAPP] Computer Systems A Programmer's Perspective](https://www.yuque.com/ob26eq/nshoar/xr3yvy)
产出目标：完成[CSAPP书籍配套的所有Labs](http://csapp.cs.cmu.edu/3e/labs.html)
挑战难度：4星
说明：这门课程是系统编程基础，也是后续操作系统/网络/数据库/编译等课程的基础，相关内容是通向系统架构师的基本功。这门课比较贴近企业实战，对动手能力要求很高，课程一大目标是要程序员写出对机器友好的高性能代码。

## 第1年下半年

课程：数据结构
参考课程：[[2020] UC Berkeley: CS 61B Data Structures](https://www.yuque.com/ob26eq/nshoar/ktft1i)
参考书籍：Head First Java + [[教材] Algorithms by Robert Sedgewick, Kevin Wayne 算法 第四版](https://www.yuque.com/ob26eq/nshoar/mz9ag8)
产出目标：完成CS 61B站点上的所有Labs/Homeworks/Projects。
挑战难度：4星
说明：数据结构的重要性毋庸置疑，伯克利的CS课程都是比较偏向实战型工程师的，纯理论的东西相对少。本课的重点是树立抽象编程思维，务必把所有Labs/Homeworks/Projects都搞定。

## 2.4 第2年上半年

课程：操作系统
参考课程：[[2020＼2018] MIT: 6.828／6.S081 Operating System Engineering](https://www.yuque.com/ob26eq/nshoar/fl2p8i)
参考书籍：[[教材] [Free] Operating Systems Three Easy Pieces 操作系统导论](https://www.yuque.com/ob26eq/nshoar/dhy6qo)
产出目标：完成MIT 6.828站点上的所有7个Labs
挑战难度：5星
说明：6.828是MIT的神课，这门课难度不小，含金量也不小。如果能把所有实验都搞定，对操作系统的认识会有质的飞跃。

## 2.5 第2年下半年

课程：计算机网络
参考课程：[[2013 FA] Stanford: CS 144 Introduction to Computer Networking](https://www.yuque.com/ob26eq/nshoar/rxfnp7)
参考书籍：[[教材] Computer Networking: A Top-Down Approach 7th 2017＼计算机网络 自顶向下方法](https://www.yuque.com/ob26eq/nshoar/fdp9hu)
产出目标：完成CS 144 站点上的所有8个Labs。
挑战难度：4星
说明：计算机网络知识和技能，是互联网应用开发的基础，也是成为系统架构师的基础。这门CS 144和配套书《计算机网络：自顶向下方法》，是目前最佳的学习计算机网络基础的课程和参考书。这也是一门投入产出比比较高的课(学了马上能用)。

## 2.6 第3年上半年

课程：编译原理
参考课程：[Stanford: CS 143 Compilers and interpreters](https://www.yuque.com/ob26eq/nshoar/ed5x0w)
参考书籍：[Crafting Interpreters](https://www.craftinginterpreters.com/contents.html) 或者 [Write an Interpreter in Go](https://www.amazon.com/Writing-Interpreter-Go-Thorsten-Ball/dp/3982016118)
产出目标：参考[Crafting Interpreters](https://github.com/munificent/craftinginterpreters)，使用Java或者golang语言(或其它你熟悉的语言)，实现Lox小型编程语言。
或者，参考[Write an Interpreter in Go](https://interpreterbook.com/)，或[Write A Compiler in Go](https://compilerbook.com/)，使用Java语言实现Monkey小型语言。
挑战难度：5星
说明：视频可以不看，但是一定要自己动手实现一个小语言解释器或者编译器。

## 2.7 第3年下半年

课程：数据库系统
参考课程：[[2019 FA] CMU: 15-445＼645 Intro to Database Systems](https://www.yuque.com/ob26eq/nshoar/ivg33v)
参考书籍：[[教材／图书] Database System Concepts 7th 2019＼数据库系统概念](https://www.yuque.com/ob26eq/nshoar/pwzbgz)
产出目标：参考[vanilladb项目](https://github.com/vanilladb/vanillacore)，使用golang语言实现clone版的vanilladb（原项目是Java实现的）。
挑战难度：5星
说明：视频/课程/书可以不看，但是一定要自己动手实现一个小型的数据库系统，包括服务器端的存储引擎、SQL解析器、查询引擎和JDBC访问接口。企业开发大部分是基于数据库的应用，如果要成为企业级架构师，必须对数据库底层实现有一定掌握。课程项目要求用golang，对golang语言不熟悉的，自己找资料自学，如果你按照课程计划坚持学到这门课，那么你已经具有足够基础，可以轻松pick up任何一门编程语言。

# 引用
[1] github 站点: [https://github.com/spring2go/cs_study_plan](https://github.com/spring2go/cs_study_plan)
[2] CSE 251 Programming in C: [https://www.cse.msu.edu/~cse251/index.html](https://www.cse.msu.edu/~cse251/index.html)
[3] CSE351: The Hardware/Software Interface: http://courses.cs.washington.edu/courses/cse351/
[4] 深入理解计算机系统(CSAPP): http://product.dangdang.com/24106647.html
[5] Washington CSE351 2017: https://www.bilibili.com/video/BV1Zt411s7Gg
[6] CSAPP书籍配套的所有Labs: http://csapp.cs.cmu.edu/3e/labs.html
[7] CS61B Data Structures: https://sp19.datastructur.es/
[8] UCB CS 61B Data Structures: https://www.bilibili.com/video/BV1EJ411n72e
[9] Operating System Engineering: https://pdos.csail.mit.edu/6.828/2018/index.html
[10] 操作系统导论(Operating Systems: Three Easy Pieces): http://product.dangdang.com/27882546.html
[11] HMC CS 134 2019 Operating System: https://www.bilibili.com/video/av47977122
[12] CS 144 Introduction to Computer Networking: https://cs144.github.io/
[13] 计算机网络：自顶向下方法: http://product.dangdang.com/25299722.html
[14] 斯坦福大学：CS144 计算机网络介绍: https://www.bilibili.com/video/BV137411Z7LR
[15] Crafting Interpreters: https://www.craftinginterpreters.com/contents.html
[16] Write an Interpreter in Go: https://www.amazon.com/Writing-Interpreter-Go-Thorsten-Ball/dp/3982016118
[17] CS143 斯坦福编译原理: https://www.bilibili.com/video/BV1cE411f78c
[18] Crafting Interpreters: https://github.com/munificent/craftinginterpreters
[19] Write an Interpreter in Go: https://interpreterbook.com/
[20] Write A Compiler in Go: https://compilerbook.com/
[21] 15-445/645 Database Systems: https://15445.courses.cs.cmu.edu/fall2020/
[22] 数据库系统概念: http://product.dangdang.com/22632572.html
[23] 卡耐基梅隆大学15-445 数据库系统介绍: https://www.bilibili.com/video/BV1Cp4y1C7dv
[24] vanilladb项目: https://github.com/vanilladb/vanillacore
[25] 自学计算机科学: https://github.com/keithnull/TeachYourselfCS-CN/blob/master/TeachYourselfCS-CN.md
[26] 自学计算机科学: https://github.com/ossu/computer-science