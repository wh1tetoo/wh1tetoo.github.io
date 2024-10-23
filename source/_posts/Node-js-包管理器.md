---
title: Node.js 包管理器
date: 2024-09-20 19:20:02
tags:
categories:
---
**npm、cnpm 和 pnpm 是三种常见的 Node.js 包管理器，主要用于安装、管理和共享 JavaScript 项目中的依赖包。它们的主要区别如下：**

##### 1. npm (Node Package Manager)
简介: npm 是 Node.js 官方的包管理工具，也是最早出现的管理工具。
优点: 官方支持，社区庞大。能与 Node.js 无缝集成。
缺点: 速度较慢: 默认使用国外的 npm registry，下载依赖时可能受网络限制。
存储效率较低: 每个项目安装依赖时会在项目的 node_modules 文件夹中创建大量的重复文件。  
安装：下载 Node.js 并安装，选择合适的版本。安装完成后，打开命令行终端并输入以下命令来确认 npm 是否安装成功：
```bash
npm -v
```
<!-- more -->
##### 2. cnpm (China npm)
简介: cnpm 是阿里巴巴团队开发的 npm 的国内镜像版本，主要目的是解决在中国大陆使用 npm 的速度问题。
优点: 速度更快，依赖于国内镜像源，下载速度大幅提升。
缺点: 本质上只是 npm 的镜像版本，功能和体验与 npm 类似，只是下载速度快。
安装：cnpm 是 npm 的国内镜像工具，安装 cnpm 前需要先安装 npm。
```bash
npm install -g cnpm --registry=https://registry.npmmirror.com
cnpm -v
```
##### 3. pnpm (Performant npm)
简介: pnpm 是一个高效的包管理器，目标是解决 npm 在存储空间上的低效问题。
优点: 高效存储: pnpm 使用硬链接（hard link）机制，共享不同项目的依赖库，避免重复下载相同的依赖，节省了磁盘空间。速度快: 由于缓存机制的改进，安装依赖的速度比 npm 快。并行安装: 它可以并行处理依赖的安装任务，进一步提升速度。
缺点: 虽然已经有较大的用户群体，但相对 npm 还是较新。
安装：
```bash
npm install -g pnpm
yarn global add pnpm  # 另外一种方式
pnpm -v
```