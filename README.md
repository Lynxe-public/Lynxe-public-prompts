# 公共用例集合

## 项目介绍

本项目包含了一系列展示系统核心功能的实用案例，涵盖了从基础查询到高级自动化工作流的各种应用场景。每个用例都提供了详细的中英文说明文档，帮助用户快速理解和掌握系统的使用方法。

## 🚀 快速启动

### 1. 下载源码
下载最新版本的 JAR 文件：访问 [Lynxe Releases 页面](https://github.com/spring-ai-alibaba/Lynxe/releases) 下载最新版本的 `lynxe.jar` 文件。

### 2. 输入 SK
访问 [阿里云百炼控制台](https://bailian.console.aliyun.com/?tab=model#/api-key)，在密钥管理页面创建 API Key 并复制密钥。运行 JAR 文件后，在浏览器中访问 `http://localhost:18080`，在引导页面输入您的 DashScope API 密钥完成配置。新用户可享受 100万Token 输入和 100万Token 输出的免费额度（有效期90天）。

### 3. 导入 Script
在系统中导入 [prompt-script](../prompt-script/) 目录下的 JSON 配置文件，系统会自动识别并加载模板配置。

### 4. 使用
在聊天对话框中选择对应的功能服务，即可开始使用各种 Func-Agent 功能。

## 用例概览

### ⭐ 高频Func-Agent推荐

#### 翻译与语法纠正
- **文件位置**: [chn/translation-grammar.md](chn/translation-grammar.md) | [eng/translation-grammar.md](eng/translation-grammar.md)
- **推荐理由**: 日常工作中作者最常用的功能之一，可以快速翻译中文到英文，并纠正英文语法和拼写错误，帮助提升英语表达能力
- **功能描述**: 智能翻译和语法纠正工具，支持中文翻译为英文，以及英文语法错误和拼写错误的自动纠正，并提供详细的语法解释和更地道的英语表达建议
- **核心特性**: 
  - 中英文双向翻译：自动识别输入语言并执行相应操作
  - 语法错误纠正：自动检测并纠正英文语法和拼写错误
  - 详细语法解释：解释各类从句、主系表、补语等语法结构
  - 地道表达建议：提供更自然、更地道的英语表达方式
  - 在对话中直接使用，操作简单便捷
- **适用场景**: 日常英语学习、文档翻译、邮件写作、语法检查、英语表达提升

#### Bing搜索问答
- **文件位置**: [chn/bing-search.md](chn/bing-search.md) | [eng/bing-search.md](eng/bing-search.md)
- **推荐理由**: 这是非常经常用的工具之一，可以快速搜索并回答各种问题
- **功能描述**: 使用MCP服务集成Bing搜索引擎，实现基于搜索结果的智能问答功能
- **核心特性**: 
  - MCP服务配置和集成
  - 在对话中直接使用，操作简单便捷
  - 基于搜索结果的智能问答
- **适用场景**: 信息搜索、智能问答、实时信息查询

---

### 产品功能介绍类Func-Agent

#### 1. Func-Agent示例
- **文件位置**: [chn/func-agent-example.md](chn/func-agent-example.md) | [eng/func-agent-example.md](eng/func-agent-example.md)
- **推荐理由**: 这是展示Function-Agent设计理念的核心示例，演示了如何通过函数组合和路由机制实现智能问题分类和专家系统
- **功能描述**: 展示函数化Agent（Function-Agent）设计理念，演示如何通过函数组合和路由机制，实现智能问题分类和专家系统
- **核心特性**:
  - Function-Agent能力：智能函数组合和自动任务分解
  - 子Agent独立记忆资源：技术专家、数据库专家、业务专家拥有完全独立的记忆资源
  - 并行使用能力：多个子Agent可以并行使用
  - 路由机制：根据问题类型自动选择最合适的处理函数
  - 函数发布和复用：所有函数都可以作为独立的工具被调用
- **适用场景**: 智能问题分类、专家系统、函数组合、任务路由

#### 2. 表单输入演示
- **文件位置**: [chn/form-input-demo.md](chn/form-input-demo.md) | [eng/form-input-demo.md](eng/form-input-demo.md)
- **推荐理由**: 展示用户交互等待机制和登录状态保持功能，是处理需要用户登录网站操作的核心示例
- **功能描述**: 展示用户交互等待机制和登录状态保持功能
- **核心特性**:
  - Form-input工具使用
  - 异步用户交互处理
  - 浏览器会话状态保持
- **适用场景**: 需要用户登录的网站操作、交互式工作流

#### 3. 图片和PDF识别演示
- **文件位置**: [chn/image-pdf-recognition.md](chn/image-pdf-recognition.md) | [eng/image-pdf-recognition.md](eng/image-pdf-recognition.md)
- **推荐理由**: 展示从网站下载PDF并解析文档的核心示例，通过导入计划模板即可使用，流程简洁
- **功能描述**: 展示PDF下载和文档解析能力，通过浏览器自动化从网站下载PDF文档，并利用文档解析工具提取结构化信息
- **核心特性**:
  - 浏览器自动化：网页导航、点击、文件下载
  - 文档解析和转换技术（markdown_converter）
  - 文件系统操作（读取、搜索）
  - 结构化数据提取
  - 动态代理模式（dynamic_agent）
  - 计划模板导入即用（download_and_analyze.json）
- **适用场景**: 文档下载、文档解析、内容提取、基金公告等结构化信息提取

#### 4. 长内容输出演示
- **文件位置**: [chn/ai-novel.md](chn/ai-novel.md) | [eng/ai-novel.md](eng/ai-novel.md)
- **推荐理由**: 展示长内容一体化输出和function-agent实现的核心示例，通过分而治之策略完成长篇内容创作，支持批量生产长文章
- **功能描述**: 展示长内容一体化输出和function-agent实现，通过分而治之策略完成长篇内容创作，支持批量生产长文章
- **核心特性**:
  - 长内容一体化输出：突破上下文限制，实现连贯的长篇内容生成
  - 分而治之策略：将复杂创作任务分解为可管理的章节单元
  - 内容连贯性保证：确保各章节间的逻辑一致性和风格统一
- **适用场景**: 内容创作、创意写作、批量文章生产、长篇文档生成

---

### 📋 场景化案例库

#### 1. 小红书搜索抓取
- **文件位置**: [chn/xiaohongshu-scraper.md](chn/xiaohongshu-scraper.md) | [eng/xiaohongshu-scraper.md](eng/xiaohongshu-scraper.md)
- **功能描述**: 展示如何使用浏览器工具、数据库工具和并发工具，实现网站搜索抓取并存储到数据库的完整流程
- **核心特性**:
  - 浏览器自动化：打开网站、搜索关键词、获取页面内容
  - 数据库操作：创建表结构、查询和存储数据
  - 并发处理：并行抓取多个链接内容
  - 用户交互等待：登录状态的处理和保持
  - 数据去重：自动检测并更新已有数据
- **适用场景**: 网站数据抓取、内容采集、信息监控、数据存储

#### 2. Bing搜索问答
- **文件位置**: [chn/bing-search.md](chn/bing-search.md) | [eng/bing-search.md](eng/bing-search.md)
- **功能描述**: 展示如何使用MCP服务集成Bing搜索引擎，实现基于搜索结果的智能问答功能
- **核心特性**:
  - MCP服务配置和集成
  - 计划模板导入和管理
  - 在对话中启用功能服务
  - 基于搜索结果的智能问答
  - 精确控制工具数量的func-agent设计理念
- **适用场景**: 信息搜索、智能问答、实时信息查询

#### 3. 图文生成与Word导出
- **文件位置**: [chn/image-word-gen.md](chn/image-word-gen.md) | [eng/image-word-gen.md](eng/image-word-gen.md)
- **功能描述**: 展示如何生成带图片的Markdown内容并导出为Word文档，实现内容创作、图片生成和文档格式转换的完整流程
- **核心特性**:
  - 内容创作：自动生成符合主题要求的长文本内容
  - 图片生成：使用wan2.6-t2i模型进行AI图片生成
  - 格式转换：将Markdown文档转换为Word格式
  - 图片插入：自动将生成的图片插入到Markdown文档的指定位置
  - 多步骤协调：通过单一函数调用完成多个步骤的自动化执行
- **适用场景**: 内容创作、文档生成、图文混排、格式转换

## 贡献指南

欢迎贡献新的用例和改进现有文档。请确保：
- 提供中英文两个版本
- 使用清晰的步骤编号
- 包含预期结果和技术要点
- 保持文档格式的一致性

## 许可证

本项目采用开源许可证，具体信息请查看LICENSE文件。

## 交流讨论

点击这个链接加入钉钉群讨论：[ding群链接](https://qr.dingtalk.com/action/joingroup?code=v1,k1,PBuFX00snERuKcnnG4YAPK52FOXwAkLYlulUUD9KiRo=&_dt_no_comment=1&origin=11)