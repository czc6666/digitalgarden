---
{"dg-publish":true,"permalink":"/czc知识库/1-计算机/编程/python笔记/多线程编程 python/","dgPassFrontmatter":true,"created":"2024-12-07T08:39:46.979+08:00","updated":"2024-12-08T12:19:23.739+08:00"}
---



> [!NOTE]- ChatGPT介绍多线程：
> 
> 当涉及到 Python 中的多线程编程时，以下是需要了解的关键知识点：
> 
> 1. **线程与进程的区别**：
>     
>     - 线程是程序执行的最小单元，进程是操作系统分配资源的最小单位。一个进程可以包含多个线程，它们共享进程的资源。
>     - 线程之间共享内存空间，进程之间通常需要通过 IPC（进程间通信）来进行数据交换。
> 2. **Python 中的多线程**：
>     
>     - Python 提供了 `threading` 模块来支持多线程编程，通过创建 `Thread` 类的实例来实现多线程。
>     - 多线程可以并发执行任务，但由于 Python 的全局解释器锁 GIL（Global Interpreter Lock），多线程在 CPU 密集型任务中无法实现真正的并行。
> 3. **多线程的应用场景**：
>     
>     - 多线程适用于 I/O 密集型任务，比如网络请求、文件读写等，因为这些任务通常会涉及等待时间，多线程可以充分利用等待时间执行其他任务。
>     - 对于 CPU 密集型任务，可以考虑使用多进程或异步编程来提高性能。
> 4. **线程的创建和管理**：
>     
>     - 创建线程可以通过继承 `threading.Thread` 类或传递可调用对象给 `Thread` 构造函数来实现。
>     - 可以使用 `start()` 方法启动线程，`join()` 方法等待线程执行完毕，`is_alive()` 方法检查线程是否在运行。
> 5. **线程间的通信**：
>     
>     - 多线程之间可以通过共享数据结构、队列等方式进行通信，但需要注意线程安全性，避免出现数据竞争和并发问题。
>     - Python 提供了 `threading.Lock` 等锁机制来确保多线程访问共享资源的安全性。
> 
> 总的来说，多线程编程可以提高程序的并发性和响应性，但需要注意线程安全性和 GIL 对并行性能的影响，合理选择多线程或其他并发模型来解决不同类型的任务。

使用的模块介绍：[python模块学习：multiprocessing模块  多线程锁](python模块学习：multiprocessing模块%20%20多线程锁.md)


## 自己在代码中见到的：
```python
# 来源：10篇方法总结里的Drebin代码
import multiprocessing as mp

processes = []  
lock = mp.Lock()




if njobs < 0:  # njobs  指并行处理的任务或作业数量，作为函数的输入
	nproc = mp.cpu_count() - 2 # 计算可用的CPU核心数并减去2（给系统留出一些资源），赋值给变量 nproc，即确定并行处理的进程数。  
	# nproc  指并行处理的进程数量
	part_size = n_files // nproc # 计算每个进程需要处理的文件数量 part_size，通过整除操作（//）获得  
else:  
	nproc = njobs  
	part_size = n_files // nproc

init_idx = 0 # 初始索引  
fin_idx = 0 # 结束索引  
for pn in range(nproc - 1):  
	init_idx = pn * part_size # 开始的位置  
	fin_idx = (pn + 1) * part_size # 结束的位置  
	processes.append( # 创建的进程对象添加到 processes 列表中  
	mp.Process(target=self._writeAPKfeatures, args=(files[init_idx:fin_idx], self._working_path, lock))  
	)  # 创建一个进程对象（目标函数=...，目标函数的参数=...，  
	processes[pn].start() # 通过 processes[pn].start() 启动这些进程进行并行处理  
  
# 这个进程也会工作，处理剩下的  
self._writeAPKfeatures(files[fin_idx:], self._working_path, lock)  
  
# 让当前进程（通常是主进程）等待指定的子进程执行完成后再继续执行后续的代码
for proc in processes:  
proc.join()
# 依次调用每个进程的 join()方法，但调用 join() 并不会暂停进程的执行
```