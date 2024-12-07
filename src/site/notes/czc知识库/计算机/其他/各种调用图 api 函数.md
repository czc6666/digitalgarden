---
{"dg-publish":true,"permalink":"/czc知识库/计算机/其他/各种调用图 api 函数/","dgPassFrontmatter":true,"created":"2024-06-18T17:45:20.923+08:00","updated":"2024-12-08T12:27:33.525+08:00"}
---


>[!note]+ 调用图--chatgpt
>调用图通常指的是在软件工程和计算机科学中用于描述代码中函数、方法或模块之间调用关系的图形表示。在这种图中，节点代表代码中的函数、方法或模块，边表示它们之间的调用关系。调用图可以帮助开发人员理解代码结构，分析程序的执行流程，并用于许多软件工程任务，如代码理解、代码优化、软件测试等。在安卓恶意软件检测中，提取应用程序的API调用图可以帮助分析应用程序的行为，识别可能的恶意行为。
>
>调用图通常有以下几种类型：
> 
> 1. **函数调用图（Function Call Graph）：** 描述程序中函数或方法之间的调用关系。每个节点代表一个函数或方法，边表示函数之间的调用关系。
>     
> 2. **方法调用图（Method Call Graph）：** 类似于函数调用图，但用于面向对象编程语言中描述类和对象方法之间的调用关系。
>     
> 3. **模块调用图（Module Call Graph）：** 描述程序中模块或文件之间的调用关系。节点代表模块或文件，边表示模块之间的调用关系。
>     
> 4. **API调用图（API Call Graph）：** 用于描述应用程序或系统中不同部分之间的API调用关系。每个节点代表一个API调用，边表示API之间的调用关系。
>     
> 5. **控制流调用图（Control Flow Call Graph）：** 不仅包括函数或方法的调用关系，还包括程序中的控制流程，如条件语句、循环语句等的执行流程。
>     
> 
> 这些调用图类型可以根据具体的应用场景和需求进行选择和使用。在安卓恶意软件检测中，常用的是API调用图，用于分析应用程序的行为模式和特征。



调用图（CG）默认指函数调用图（FCG）  

> [!NOTE] 调用图和API调用图区别
> 调用图（Call Graph）和 API 调用图（API Call Graph）是软件工程中常见的两种图形结构，用于表示程序代码中的函数调用关系和 API 调用关系。它们在代码分析、性能优化、安全检查等方面具有重要的应用价值。
> 
> 1. **函数调用图（Function Call Graph）：** 函数调用图是描述程序中函数之间调用关系的图形结构。在调用图中，节点代表函数或方法，边代表函数之间的调用关系。例如，如果函数 A 调用了函数 B，则调用图中会有一条从节点 A 到节点 B 的边。调用图可以帮助开发者理解代码的结构、调用路径和依赖关系，有助于代码分析、性能优化和代码重构等工作。
>     
> 2. **API 调用图（API Call Graph）：** API 调用图是描述程序中 API 调用关系的图形结构。在 API 调用图中，节点代表 API 函数或方法，边代表 API 之间的调用关系。API 调用图可以帮助开发者理解程序中使用的外部库、框架或服务的调用关系，有助于分析程序的依赖关系、安全漏洞和性能瓶颈。
>     
> 
> 这两种图形结构在代码分析和软件工程中有着广泛的应用。通过分析调用图和 API 调用图，开发者可以深入了解程序的结构和运行时行为，从而进行代码优化、安全检查、漏洞分析等工作。常见的工具如 Androguard、Ghidra、IDA Pro 等可以用来生成和分析调用图和 API 调用图。

