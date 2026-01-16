---
title: 从零到一：如何用 Obsidian + Quartz 打造属于你的“数字花园”
date: 2026-01-16 09:15:40
tags:
  - 技术笔记
  - 个人成长
summary: ""
slug: ""
draft: false
---
**Table of Contens**

1. [[#摘要|摘要]]
2. [[#一、 为什么是 Obsidian + Quartz？|一、 为什么是 Obsidian + Quartz？]]
3. [[#二、 环境准备与初始化|二、 环境准备与初始化]]
	1. [[#二、 环境准备与初始化#1. 安装依赖|1. 安装依赖]]
	2. [[#二、 环境准备与初始化#2. 初始化 Quartz 项目|2. 初始化 Quartz 项目]]
4. [[#三、 本地预览与调试|三、 本地预览与调试]]
	1. [[#三、 本地预览与调试#1. 本地编译|1. 本地编译]]
	2. [[#三、 本地预览与调试#2. 本地预览|2. 本地预览]]
5. [[#四、 推送至 GitHub|四、 推送至 GitHub]]
6. [[#五、 Vercel 自动构建与发布|五、 Vercel 自动构建与发布]]
7. [[#六、 自定义域名（进阶）|六、 自定义域名（进阶）]]
8. [[#相关链接|相关链接]]

![[quartz + vercel 构建博客网站 - visual selection.svg]]

## 摘要

在信息碎片化的时代，构建一个可公开、可交互的知识库（数字花园）已成为深度学习者的标配。本文将带你深度解析如何利用 [Quartz](https://quartz.jzhao.xyz/) 将 Obsidian 的本地笔记转化为高颜值的静态网站，实现“本地记录，全球同步”的无缝写作流程。

---

## 一、 为什么是 Obsidian + Quartz？

作为一名 Obsidian 重度使用者，我一直在寻找一种 **“零摩擦”** 的发布方案。传统的博客系统往往存在以下痛点：

- **发布成本高：** 需要手动导出 Markdown，处理图片路径。
    
- **生态割裂：** 无法原生支持 Obsidian 的双向链接（`[[Link]]`）和关系图谱。
    
- **体验沉重：** 像 WordPress 这样的系统维护复杂，且不支持离线写作。
    

**[Quartz 4.0](https://quartz.jzhao.xyz/)** 的出现完美解决了这些问题。它是一个基于 TypeScript 的快速静态站点生成器，其核心优势在于：

1. **原生双链支持：** 完美“翻译” Obsidian 的双链、悬浮预览和关系图谱。
    
2. **极速性能：** 极高的渲染速度和极佳的 SEO 表现。
    
3. **高度可定制：** 允许通过配置轻松更改布局、配色和功能组件。
    

---

## 二、 环境准备与初始化

在开始之前，请确保电脑已安装 [Node.js](https://nodejs.org/) (建议 LTS 版本) 和 [Git](https://git-scm.com/)。

### 1. 安装依赖

```bash
npm i
```
### 2. 初始化 Quartz 项目

将 [Quartz 源码](https://github.com/jackyzha0/quartz)，下载到本地 Obsidian 仓库中。
```
git clone https://github.com/jackyzha0/quartz.git
```

在 quartz 根目录下，打开终端，运行以下命令来创建花园骨架：

```Bash
npx quartz create
```

**交互选项说明：**

- **Project Name:** 你的项目文件夹名称。
    
- **Content Source:** 选择 `Link a folder`，并指向你 Obsidian Vault 的路径，选择默认就是content 文件夹，将笔记放在此文件夹下即可。
    
- **Links:** 建议选择 `Obsidian` 风格以保持兼容性。

---

## 三、 本地预览与调试

在将笔记推送到云端之前，我们需要在本地查看效果。

### 1. 本地编译

在项目根目录下运行编译命令：

```
npx quartz build --serve
```

**如果看到以下输出：**

> `Started serve on http://localhost:8081`

**那就成功了！** 你可以直接打开浏览器访问。

### 2. 本地预览

打开浏览器访问 `http://localhost:8080`。 Obsidian 中写的每一篇笔记、每一个双链都已经转化为了精美的网页。

---

## 四、 推送至 GitHub

Obsidian 提供了 git 插件，可以很方便的将整个仓库同步到自己的 github 账户上。具体操作有很多教程，这里就不在赘述了。

---

## 五、 Vercel 自动构建与发布

为了让全球用户都能访问这个数字花园，可以使用 [Vercel](https://vercel.com/) 进行托管。它是目前最优秀的静态部署平台之一，且对个人用户免费。

1. 登录 **Vercel** 并关联 GitHub 账号。
    
2. 点击 **"Add New Project"**，选择你刚才创建的 GitHub 仓库。
    
3. **配置构建设置：**
    
    - **Framework Preset:** 保持 `Other` 或 `Next.js` (Quartz 会被自动识别)。
        
    - **Build Command:** `npx quartz build`
        
    - **Output Directory:** `public`
        
4. 点击 **"Deploy"**。
    

一旦部署完成，以后你每次在 Obsidian 中写完笔记并推送到github上之后，Vercel 都会自动触发构建，网站会在 1-2 分钟内完成更新。

---

## 六、 自定义域名（进阶）

如果你拥有自己的域名，可以让你的数字花园更具个人色彩：

1. 在 Vercel 项目控制面板中，进入 **Settings > Domains**。
    
2. 输入你的域名（如 `blog.yourname.com`）。
    
3. 根据 Vercel 提供的提示，前往你的域名服务商（如阿里云、腾讯云或 Cloudflare）添加一条 **CNAME** 记录。
    
4. 等待解析生效，你的数字花园就正式“开张”了！
    

---

## 相关链接

[[Vercel应用绑定阿里云域名操作方法]]；




