---
{"dg-publish":true,"permalink":"/czc知识库/1-计算机/编程/java笔记/JRE 与 JDK的区别/","dgPassFrontmatter":true,"created":"2024-12-07T08:39:46.876+08:00","updated":"2024-12-08T12:18:10.603+08:00"}
---


[JRE 与 JDK的区别 | 菜鸟教程](https://www.runoob.com/w3cnote/the-different-of-jre-and-jdk.html)

> [!NOTE]
> ### 1. 定义
> 
> **JRE(Java Runtime Enviroment)** 是 Java 的运行环境。面向 Java 程序的使用者，而不是开发者。如果你仅下载并安装了 JRE，那么你的系统只能运行 Java 程序。JRE 是运行 Java 程序所必须环境的集合，包含 JVM 标准实现及 Java 核心类库。它包括 Java 虚拟机、Java 平台核心类和支持文件。它不包含开发工具(编译器、调试器等)。
> 
> JDK(Java Development Kit) 又称 J2SDK(Java2 Software Development Kit)，是 Java 开发工具包，它提供了 Java 的开发环境(提供了编译器 javac 等工具，用于将 java 文件编译为 class 文件)和运行环境(提 供了 JVM 和 Runtime 辅助包，用于解析 class 文件使其得到运行)。如果你下载并安装了 JDK，那么你不仅可以开发 Java 程序，也同时拥有了运行 Java 程序的平台。JDK 是整个 Java 的核心，包括了 Java 运行环境(JRE)，一堆 Java 工具 tools.jar 和 Java 标准类库 (rt.jar)。
> 
> ### 2. 区别
> 
> JRE 主要包含：java 类库的 class 文件(都在 lib 目录下打包成了 jar)和虚拟机(jvm.dll)；JDK 主要包含：java 类库的 class文件(都在 lib 目录下打包成了 jar)并自带一个 JRE。那么为什么 JDK 要自带一个 JRE 呢？而且 jdk/jre/bin 下的 client 和 server 两个文件夹下都包含 jvm.dll(说明 JDK 自带的 JRE 有两个虚拟机)。
> 
> **记得在环境变量 path 中设置 jdk/bin 路径吗？**老师会告诉大家不设置的话 javac 和 java 是用不了的。确实 jdk/bin 目录下包含了所有的命令。可是有没有人想过我们用的 java 命令并不是 jdk/bin 目录下的而是 jre/bin 目录下的呢？不信可以做一个实验，大家可以把 jdk/bin 目录下的 java.exe 剪切到别的地方再运行 java 程序，发现了什么？一切 OK！(JRE 中没有 javac 命令，原因很简单，它不是开发环境)那么有人会问了？我明明没有设置 jre/bin 目录到环境变量中啊？试想一下如果 java 为了提供给大多数人使用，他们是不需要 jdk 做开发的，只需要 jre 能让 java 程序跑起来就可以了，那么每个客户还需要手动去设置环境变量多麻烦啊？所以安装jre的时候安装程序自动帮你把 jre 的 java.exe 添加到了系统变量中，验证的方法很简单，去 Windows/system32 下面去看看吧，发现了什么？有一个 java.exe。
> 
> ### 3. 难点
> 
> 如果安装了 JDK，会发现你的电脑有两套 JRE，一套位于 **C:\Program Files\Java\jre6**， 另外一套位于 **C:\Program Files\Java\jdk1.6.0_41\jre** 目录下。
> 
> JRE 的地位就象一台 PC 机一样，我们写好的 Win32 应用程序需要操作系统帮我们运行，同样的，我们编写的 Java 程序也必须要 JRE 才能运行。所以当你装完 JDK 后，如果分别在硬盘上的两个不同地方安装了两套 JRE，那么你可以想象你的电脑有两台虚拟的 Java PC 机，都具有运行 Java 程序的功能。所以我们可以说，只要你的电脑安装了 JRE，就可以正确运行 Java 应用程序。
> 
> **1、为什么Sun要让JDK安装两套相同的JRE？**
> 
> 这是因为 JDK 里面有很多用 Java 所编写的开发工具，如 javac.exe、jar.exe 等，这些命令放置在 C:\Program Files\Java\jdk1.6.0_41\bin 目录里。
> 
> 因为他们是 java 编写的命令，所以要依靠 java 的 jar 包，这些 jar 包存放在 **C:\Program Files\Java\jdk1.6.0_41\lib** 目录里。
> 
> 如果将 C:\Program Files\Java\jdk1.6.0_41\lib\ 目录里面的 tools.jar 改名为 tools1.jar，然后运行 javac.exe，显示如下结果：
> 
> Exception in thread "main" java.lang.NoClassDefFoundError: com/sun/tools/javac /Main 
> 
> 但是输入:
> 
> java -cp C:\Program Files\Java\jdk1.6.0_41\lib\tools1.jar com.sun.tools.javac.Mainx
> 
> 会得到与 javac.exe 相同的结果。
> 
> 从这里我们可以证明 javac.exe 只是一个包装器（Wrapper），而制作的目的是为了让开发者免于输入太长的指命。
> 
> 而且我们可以发现 C:\Program Files\Java\jdk1.6.0_41\bin 目录下的程序都很小，不大于 29K，从这里我们可以得出一个结论。就是 JDK 里的工具几乎是用 Java 所编写，所以也是 Java 应用程序，因此要使用 JDK 所附的工具来开发 Java 程序，也必须要自行附一套 JRE 才行，所以位于C:\Program Files\Java\jdk1.6.0_41\jre 目录下的那套 JRE 就是用来运行一般 Java 程序用的。
> 
> **2、如果一台电脑安装两套以上的 JRE，谁来决定呢？**
> 
> 这个重大任务就落在 java.exe 身上。java.exe 的工作就是找到合适的 JRE 来运行 Java 程序。 java.exe 依照底下的顺序来查找 JRE：自己的目录下有没有 JRE；父目录有没有 JRE；查询注册表：
> 
> [HKEY_LOCAL_MACHINE\SOFTWARE\JavaSoft\Java Runtime Environment] 
> 
> 所以 java.exe 的运行结果与你的电脑里面哪个 JRE 被执行有很大的关系。
> 
> > 文章出处：http://swiftlet.net/archives/639