---
{"dg-publish":true,"permalink":"/czc知识库/计算机/编程/软件开发笔记/AndroZoo数据集下载器/笔记：AndroZoo数据集下载程序 筛选超大csv文件 制作下载链接 多线程下载 apk文件 python笔记/","dgPassFrontmatter":true,"created":"2024-12-07T08:39:46.862+08:00","updated":"2024-12-08T12:19:40.994+08:00"}
---


# 代码功能
- pandas读取超大型csv文件（带进度显示）
- 数据筛选
- 多线程下载

# 需求：

- 在AndroZoo申请通过使用权限，获取到官方发给你的api
- 下载AndroZoo官网最新的app列表文件：latest.cs

# 代码：
最新的组合下载链接并多线程下载函数：
```python
# 多线程下载 APK 文件
def czc_download_apk_multithreaded(apikey, filtered_file, output_dir, target_count=10000, num_threads=200):
    debug_print('开始多线程下载 APK')
    filtered_conditions = os.path.splitext(os.path.basename(filtered_file))[0]
    downloaded_file = os.path.join(output_dir, f'已下载apk_{filtered_conditions}.txt')
    if not os.path.exists(downloaded_file):
        open(downloaded_file, 'w').close()
    with open(filtered_file, 'r') as f:
        sha256_list = f.readlines()
    sha256_list = [sha.strip() for sha in sha256_list]
    def download_task(sha256, pbar):
        url = f"https://androzoo.uni.lu/api/download?apikey={apikey}&sha256={sha256}"
        debug_print(f'尝试下载 APK：{sha256}')
        try:
            response = requests.get(url, verify=True, timeout=10)
            if response.status_code == 200:
                apk_name = sha256 + '.apk'
                with open(os.path.join(download_dir, apk_name), 'wb') as file:
                    file.write(response.content)
                with open(downloaded_file, 'a') as f:
                    f.write(sha256 + '\n')
                pbar.update(1)
                debug_print(f'下载成功：{sha256}')
            else:
                debug_print(f'下载失败：{sha256}, 状态码：{response.status_code}')
        except Exception as e:
            debug_print(f'下载错误：{sha256}，错误信息：{e}')
    while True:
        with open(downloaded_file, 'r') as f:
            downloaded_list = f.readlines()
        downloaded_list = [sha.strip() for sha in downloaded_list]
        if len(downloaded_list) >= target_count:
            debug_print(f'下载任务完成，已下载 {len(downloaded_list)} 个 APK')
            break
        to_download = list(set(sha256_list) - set(downloaded_list))
        random.shuffle(to_download)
        download_dir = os.path.join(output_dir, 'apks')
        os.makedirs(download_dir, exist_ok=True)
        debug_print(f'下载目录已创建：{download_dir}')
        with tqdm(total=target_count, desc='下载进度', initial=len(downloaded_list)) as pbar:
            with ThreadPoolExecutor(max_workers=num_threads) as executor:
                futures = []
                while len(downloaded_list) < target_count and to_download:
                    sha256 = to_download.pop()
                    future = executor.submit(download_task, sha256, pbar)
                    futures.append(future)
                    downloaded_list.append(sha256)
                for future in futures:
                    future.result()
    debug_print('多线程下载完成')
```

最新的代码在台式里

```python
import os
import requests
from datetime import datetime
import pandas as pd
from concurrent.futures import ThreadPoolExecutor
import time
from tqdm import tqdm
import gc

debug = True
apikey = '58b1fe025f2e5ab21ebb282515415dea1eeb28985d9083c0a397e7eda08ea8f8'  # czc api
# apikey = '77aec76df8b564d8b46de4b1ec775764188dcee2c768510a559bd535c88f5cc9'  # zky api

# 带有进度显示的读取csv文件函数
def czc_read_csv(path, chunksize=100000, parse_dates=['dex_date']):
    starttime = time.perf_counter()
    chunks = []
    for chunk in tqdm(pd.read_csv(path, parse_dates=parse_dates, chunksize=chunksize)):
        chunks.append(chunk)
    df = pd.concat(chunks, ignore_index=True)
    endtime = time.perf_counter()
    print('读取完毕，用时：', endtime - starttime)
    return df

# 从读取的到的csv文件按需求随机筛选数据
def filter_apk(config, output_dir, csv_path='latest.csv', random_selection=False, random_sample_size=0):
    start_year_filter = config['start_year']
    end_year_filter = config['end_year']
    dex_size_limit = config['dex_size_limit']
    apk_size_limit = config['apk_size_limit']
    print('文件读取中')
    df = czc_read_csv(csv_path, parse_dates=['dex_date'])
    df.set_index('dex_date', inplace=True)
    # 筛选数据
    print('筛选 APK 中')
    filtered_df = df.loc[(df.index.year >= start_year_filter) & (df.index.year <= end_year_filter) & (df['vt_detection'] == 0) & (df['dex_size'] < dex_size_limit) & (df['apk_size'] < apk_size_limit)]

    # 随机抽样
    if random_selection:
        if random_sample_size < len(filtered_df):
            # 仅当随机抽样量小于数据总量时才进行抽样
            filtered_df = filtered_df.sample(n=random_sample_size)
    filtered_df.to_csv(os.path.join(output_dir, 'filtered_apks.csv'), index=False)
    del df  # 删除df释放内存
    gc.collect()  # 强制进行垃圾回收
    return filtered_df

# 根据筛选后的数据制作下载链接输出到txt文件
def generate_download_link(filtered_df, out_dir, split_size=1000000):
    # 创建下载链接目录
    links_dir_name = os.path.join(out_dir, 'links')
    os.makedirs(links_dir_name, exist_ok=True)
    # 拆分下载链接并保存到多个TXT文件
    print('链接生成中')
    num_rows = filtered_df.shape[0]
    for i in range(0, num_rows, split_size):
        chunk_df = filtered_df.iloc[i:i + split_size]
        links_file = os.path.join(links_dir_name, f'links_{i // split_size + 1}.txt')
        with open(links_file, 'w') as f:
            for sha_value in chunk_df['sha256']:
                link = f"https://androzoo.uni.lu/api/download?apikey={apikey}&sha256={sha_value}\n"
                f.write(link)
    del filtered_df  # 删除filtered_df释放内存
    gc.collect()  # 强制进行垃圾回收
    return links_dir_name

def download_apk(url, download_path, pbar):
    try:
        while 1:
            response = requests.get(url, verify=True)
            if response.status_code == 200:
                apk_name = url.split('=')[-1] + '.apk'
                with open(os.path.join(download_path, apk_name), 'wb') as file:
                    file.write(response.content)
                pbar.set_postfix_str(f'已下载: {apk_name}')
                pbar.update(1)
                break
            time.sleep(1)
    except Exception as e:
        pbar.set_postfix_str(f'下载错误: {url}: {e}')
        pbar.update(1)

def download_apk_multithreaded(links_dir, output_dir, num_threads=200):
    download_dir = os.path.join(output_dir, 'apks')
    os.makedirs(download_dir, exist_ok=True)
    all_download_links = []
    for txt_file in os.listdir(links_dir):
        with open(os.path.join(links_dir, txt_file), 'r') as file:
            download_links = file.readlines()
            all_download_links.extend([link.strip() for link in download_links])
    with tqdm(total=len(all_download_links), desc='下载进度') as pbar:
        with ThreadPoolExecutor(max_workers=num_threads) as executor:
            futures = [executor.submit(download_apk, link, download_dir, pbar) for link in all_download_links]
            for future in futures:
                future.result()

def re_download(output_dir, num_threads=1):
    links_dir = os.path.join(output_dir, 'links')
    apks_dir = os.path.join(output_dir, 'apks')
    all_links = []
    for txt_file in os.listdir(links_dir):
        with open(os.path.join(links_dir, txt_file), 'r') as file:
            download_links = file.readlines()
            all_links += [link.strip()[-64:] for link in download_links]
    all_apks = [apk[:-4] for apk in os.listdir(apks_dir)]
    failed_apk_downloads = list(set(all_links).difference(set(all_apks)))
    failed_apk_downloads_df = pd.DataFrame({'sha256': failed_apk_downloads})
    print(f'共 {len(failed_apk_downloads)} 个 APK 下载失败')
    re_download_dir = os.path.join(output_dir, datetime.now().strftime("%Y_%m_%d_%H_%M_redownload"))
    os.makedirs(re_download_dir, exist_ok=True)
    print('重新生成下载链接')
    re_download_links_dir = generate_download_link(failed_apk_downloads_df, out_dir=re_download_dir)
    print('开始重新下载')
    download_apk_multithreaded(re_download_links_dir, re_download_dir, num_threads=num_threads)

def debug_print(a):
    if debug: print(a)
  
if __name__ == '__main__':
    configs = {
        'start_year': 2014,
        'end_year': 2014,
        'dex_size_limit': 500 * 1024,
        'apk_size_limit': 1024 * 1024 * 1024
    }
    output_dir = datetime.now().strftime("%Y%m%d")
    output_dir += '_' + '_'.join([str(configs[c]) for c in configs])
    debug_print('生成下载目录名字')
    os.makedirs(output_dir, exist_ok=True)
    debug_print('创建下载目录完成')
    df = filter_apk(configs, output_dir, random_selection=True, random_sample_size=40000)
    debug_print('apk过滤完成')
    links_dir = generate_download_link(df, output_dir)
    debug_print('下载链接txt生成完成')
    debug_print('开始多线程下载')
    download_apk_multithreaded(links_dir, output_dir, num_threads=200)
```