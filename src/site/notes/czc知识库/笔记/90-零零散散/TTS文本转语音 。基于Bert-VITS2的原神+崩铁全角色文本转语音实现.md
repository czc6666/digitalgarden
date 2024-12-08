---
{"dg-publish":true,"permalink":"/czc知识库/笔记/90-零零散散/TTS文本转语音 。基于Bert-VITS2的原神+崩铁全角色文本转语音实现/","dgPassFrontmatter":true,"created":"2024-06-18T17:45:22.460+08:00","updated":"2024-12-08T11:36:08.858+08:00"}
---


TTS：Text To Speech 文本转语音
基于Bert-VITS2的原神+崩铁全角色文本转语音实现 
## 基于Bert-VITS2的原神+崩铁全角色文本转语音实现 
b站up主：Stardust_减

视频地址： https://www.bilibili.com/video/BV1hp4y1K78E

github仓库地址： https://github.com/Stardust-minus/Bert-VITS2

在线合成使用网址：[v2.genshinvoice.top](https://v2.genshinvoice.top)

同时这里已经裁切了一份Bert-VITS2的底模，仅可用于训练，无法推理。 https://openi.pcl.ac.cn/Stardust_minus/Bert-VITS2/modelmanage/model_readme_tmpl?name=Bert-VITS2%E4%B8%AD%E6%97%A5%E5%BA%95%E6%A8%A1
从github加了qq群
20231200@全体成员 在线服务已与仓库主线版本同步，更换为gradio webui。原接口不再计划维护，不保证可用性，请使用API的各位及时迁移到gradio client。新地址 。原版API仍在运行，但由于**目前有大量请求在攻击后端API**，可能出现访问异常缓慢的情况。
找的别人的部署本地的视频： https://www.bilibili.com/video/BV15j411j7Jz
## [Text To Speech - 在线文本转语音 (text-to-speech.cn)](https://www.text-to-speech.cn/)
网上随便找的，貌似调用的微软的api。每天限制2000字
A Speech service feature that converts text to lifelike speech
## [原神语音合成 - MikuTools (okmiku.com)](https://okmiku.com/anime_tts)
网上找的另一个。负载好像很高，用不了 。傻逼网站，几个字慢的要死，还限制25字