---
{"dg-publish":true,"permalink":"/czc知识库/计算机/搞机/Windows/老笔记/bat-重启资源管理器bat脚本/","dgPassFrontmatter":true,"created":"2024-06-18T17:45:20.288+08:00","updated":"2024-12-08T12:34:13.018+08:00"}
---


@echo off
taskkill /f /im explorer.exe
start explorer.exe