---
{"dg-publish":true,"permalink":"/czc知识库/5-就业/Python/python学习/0-模块/python模块-tqdm，进度条 可视化/","dgPassFrontmatter":true,"created":"2024-12-07T08:39:46.910+08:00","updated":"2024-12-08T12:19:23.665+08:00"}
---


# Python 动态进度条实现
[# Python 动态进度条实现](https://mp.weixin.qq.com/s/LeoD-nzY-kRq5PomH9oisw)
↑文章实现的效果
```
Progress: [--------------------->] 100%
---
Processing: 100%|██████████| 50/50 [00:05<00:00, 9.82it/s]
---
Processing: 50/50 [00:05<00:00, 9.82it/s]
---
First: 100%|██████████| 100/100 [00:05<00:00, 19.31it/s]
Second: 100%|██████████| 100/100 [00:05<00:00, 19.31it/s]
---
Processing: 100%|██████████| 50/50 [00:05<00:00, 9.82it/s]
---
Processing 50: 100%|██████████| 50/50 [00:05<00:00, 9.82it/s]
---
Progress: 100% completed.
---
Processing... 100% 50/50 [00:05<00:00, 9.82it/s]
```


# 两种多线程的进度条

```python
from concurrent.futures import ThreadPoolExecutor, as_completed
from tqdm import tqdm
```

这两个进度条的主要区别在于它们所应用的上下文和功能：

1. **ThreadPoolExecutor + tqdm**：
    
    - **功能**：用于并发任务管理和显示每个任务的进度。
    - **应用场景**：适用于需要同时处理多个任务，并希望在任务执行过程中显示整体进度的情况。例如，批量处理文件、并行计算等场景。
    - **特点**：能够显示每个任务的执行进度，但通常是针对整体任务组的执行进度，而非单个任务的细节进度。
2. **as_completed + tqdm**：
    
    - **功能**：用于跟踪并发任务中每个任务的完成情况，并显示整体任务组的进度。
    - **应用场景**：适用于需要跟踪并发任务中每个任务完成情况的情况。通常用于需要单独监控每个任务状态或处理每个任务结果的场景。
    - **特点**：能够实时显示每个任务的完成情况，适合需要更详细任务监控和控制的情况。

**选择使用哪种进度条取决于你的具体需求**：

- 如果你只需监控整体任务组的进度，并发任务之间相对独立，那么 `ThreadPoolExecutor + tqdm` 是一个简单有效的选择。
- 如果你需要更细粒度地控制每个任务的执行状态，或者需要根据单个任务的完成情况作进一步处理，那么可以考虑使用 `as_completed + tqdm` 的方式。

综上所述，两种方法在不同的并发任务管理和监控需求中有各自的优劣和适用性。

我只需监控整体任务组的进度，并发任务之间相对独立，请用 ThreadPoolExecutor + tqdm 写一遍


## gpt给的例子

好的，下面我将分别给出使用 `ThreadPoolExecutor + tqdm` 和 `as_completed + tqdm` 的示例代码，以便你可以学习它们的用法和区别。

### 使用 ThreadPoolExecutor + tqdm 示例

```python
import concurrent.futures
from tqdm import tqdm
import time

def task(name):
    # 模拟耗时任务
    time.sleep(1)
    return f"Task {name} completed"

def main():
    tasks = ["Task 1", "Task 2", "Task 3", "Task 4", "Task 5"]

    with concurrent.futures.ThreadPoolExecutor(max_workers=3) as executor:
        results = []
        with tqdm(total=len(tasks), desc="Processing tasks") as pbar:
            futures = {executor.submit(task, task_name): task_name for task_name in tasks}
            for future in concurrent.futures.as_completed(futures):
                result = future.result()
                results.append(result)
                pbar.update(1)
    
    print("All tasks completed:")
    for result in results:
        print(result)

if __name__ == "__main__":
    main()

```

**说明**：

- **功能**：该示例使用 `ThreadPoolExecutor` 并结合 `tqdm` 实现对多个任务的并发执行，并显示整体进度条。
- **应用场景**：适用于批量处理任务，例如批量下载文件、并行处理数据等。
- **特点**：进度条显示的是整体任务的进度，无法在进度条上看到单个任务的详细执行情况。

### 使用 as_completed + tqdm 示例

```python
import concurrent.futures
from tqdm import tqdm
import time

def task(name):
    # 模拟耗时任务
    time.sleep(1)
    return f"Task {name} completed"

def main():
    tasks = ["Task 1", "Task 2", "Task 3", "Task 4", "Task 5"]

    with concurrent.futures.ThreadPoolExecutor(max_workers=3) as executor:
        results = []
        futures = [executor.submit(task, task_name) for task_name in tasks]
        
        with tqdm(total=len(futures), desc="Processing tasks") as pbar:
            for future in concurrent.futures.as_completed(futures):
                result = future.result()
                results.append(result)
                pbar.update(1)
    
    print("All tasks completed:")
    for result in results:
        print(result)

if __name__ == "__main__":
    main()
```

**说明**：

- **功能**：该示例使用 `as_completed` 和 `tqdm` 实现对多个任务的并发执行，并显示每个任务的完成情况。
- **应用场景**：适用于需要监控每个任务状态或对每个任务结果进行处理的情况。
- **特点**：进度条能够实时显示每个任务的完成情况，便于详细监控和处理每个任务的执行结果。

这两个示例展示了如何使用不同的并发任务管理方式结合 `tqdm` 实现进度条的功能，以满足不同的需求场景。