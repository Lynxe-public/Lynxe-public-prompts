# 公共用例集合

## 项目介绍

本项目包含了一系列展示系统核心功能的实用案例，涵盖了从基础查询到高级自动化工作流的各种应用场景。每个用例都提供了详细的中英文说明文档，帮助用户快速理解和掌握系统的使用方法。

## 用例概览

### ⭐ 高频Func-Agent推荐

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
- **推荐理由**: 展示图片和PDF识别功能的核心示例，支持批量识别和结构化输出，同时支持HTTP接口调用
- **功能描述**: 展示图片和PDF识别功能，支持批量识别和结构化输出，同时支持HTTP接口调用
- **核心特性**:
  - 文档解析和OCR技术
  - 结构化数据提取
  - HTTP服务发布和调用
  - 文件上传和批量处理
  - 异步任务执行
  - JSON格式标准化输出
- **适用场景**: 文档处理、内容提取、批量识别、API服务

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

## 技术架构

### 核心组件
- **Func-Agent模式**: 系统的主要工作模式，支持复杂任务规划和执行
- **工具集成**: 内置browser_use工具和外部MCP服务集成
- **函数组合**: 支持将复杂任务分解为可复用的工具函数
- **状态管理**: 支持浏览器会话和登录状态的持久化

## 文件结构

```
public-usecase/
├── README.md                    # 项目总览（本文件）
├── README_EN.md                # 英文版项目总览
├── chn/                        # 中文版用例文档
│   ├── stock-price-query.md    # 股票价格查询
│   ├── form-input-demo.md     # 表单输入演示
│   ├── query-plan.md          # 函数化Agent
│   ├── image-pdf-recognition.md # 图片和PDF识别
│   ├── ai-novel.md           # AI小说
│   ├── bing-search.md        # Bing搜索问答
│   ├── func-agent-example.md # 函数化Agent示例
│   ├── image-word-gen.md    # 图文生成与Word导出
│   └── xiaohongshu-scraper.md # 小红书搜索抓取
└── eng/                       # 英文版用例文档
    ├── stock-price-query.md   # Stock Price Query
    ├── form-input-demo.md    # Form Input Demo
    ├── query-plan.md         # Functional Agent
    ├── image-pdf-recognition.md # Image and PDF Recognition
    ├── ai-novel.md          # AI Novel
    ├── bing-search.md       # Bing Search Q&A
    ├── func-agent-example.md # Function-Agent Example
    └── xiaohongshu-scraper.md # Xiaohongshu Search Scraping
```

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