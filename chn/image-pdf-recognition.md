# 图片和PDF识别

## 介绍
图片和PDF识别是AI Agent的一个非常常用的功能需求。本系统支持图片与PDF的批量识别并按要求做结构化输出，同时也支持用接口调用的方式来使用图像识别。通过这个用例，用户可以学习如何构建文档解析能力并将其发布为可复用的服务。

## Func-Agent增强模式

### 说明
本例子使用增强的func-agent来实现图片和PDF识别功能，展示如何构建结构化的文档解析能力并发布为HTTP服务

### 具体步骤

#### 第一部分：构建结构化的PDF/图片解析能力

**第1步** 进入Func-Agent计划模式
- 在首页，点击系统右下角的func-agent计划模式
- 在左边会出现一个新的框"Func-agent计划模板"

**第2步** 创建新计划
- 点击"新建计划"按钮

**第3步** 配置计划模板
- 点击"添加第一个步骤"
- 依次输入以下信息：
  - **计划模板名字**：`识别图片为根基的PDF文件`
  - **任务需求**：
    ```
    依托上传上来的PDF/jpeg文件，回答如下关键问题：
    本文件的前100个字，以及最后的100个字，分别是什么（你可以改为你自己的分析需求）
    ```
  - **任务的输出要求**：`位置(前/后),详细内容`

**第4步** 选择工具
- 点击"添加/删除工具"按钮
- 选择以下工具：
  - `markdown_converter`工具
  - `global_file_operator`工具

**第5步** 保存计划
- 点击"save"按钮
- 等待提示"保存成功"

**第6步** 上传文件
- 点击"附加文件"按钮
- 选择一个图片文件或需要OCR能力的PDF文件
- 确认文件上传成功

**第7步** 执行计划
- 点击"执行计划"按钮
- 观察系统对文件进行识别和解析的过程
- 查看初步输出结果

#### 第二部分：发布为HTTP服务并实现远程调用

**第8步** 发布为工具服务
- 点击左边栏最下面的"发布为工具服务"
- 依次填入以下信息：
  - **工具名称**：`pdf_recognizer`
  - **工具描述**：`可以用来做pdf的自动识别`
  - **服务组**：`document-reader`（可以替换为方便管理的名称）
- 选择"发布为内部工具调用"和"发布为HTTP服务"
- 点击"发布为服务"

**第9步** 查看调用示例
- 系统会显示多种调用方式的示例
- 提供get+sync、post+sync、post+async几种调用方式
- 建议使用post+sync进行调试

**第10步** 文件上传调用
- 使用POST方法上传文件：
  ```bash
  curl -X POST \
    -F "files=@/path/to/your/file.pdf" \
    http://localhost:18080/api/file-upload/upload
  ```
- 预期返回结果：
  ```json
  {
    "success": true,
    "message": "Files uploaded successfully",
    "uploadKey": "upload-1760933409277_77_50",
    "uploadedFiles": [
      {
        "originalName": "your/file.pdf",
        "size": 262219,
        "type": "application/pdf",
        "uploadTime": [2025,10,20,12,10,9,278841000],
        "success": true
      }
    ]
  }
  ```

**第11步** 执行识别任务
- 使用uploadKey作为参数，调用post+async方法：
  ```bash
  POST /api/executor/executeByToolNameSync
  Content-Type: application/json
  
  {
    "toolName": "pdf_recognizer",
    "replacementParams": {
      "rawParam": "test"
    },
    "uploadedFiles": ["upload-1760933409277_77_50"]
  }
  ```
- **注意**: `"upload-1760933409277_77_50"` 是上面步骤返回的uploadKey示例值，实际调用时需要替换为第10步返回的真实uploadKey值
- **参数说明**: `replacementParams` 中的 `"rawParam": "test"` 仅用于演示，实际传递这个值没有意义。如果系统里有要求传入参数，那么可以用这个方式传入
- 预期返回结果：
  ```json
  {
    "status": "completed",
    "result": "Execution result here"
  }
  ```

**第12步** 验证结果
- 检查返回的JSON标准化结果
- 确认文档解析功能正常工作
- 验证结构化输出格式

## 预期结果
- 成功构建PDF/图片识别能力
- 系统能够解析文档内容并提取关键信息
- 发布为可复用的HTTP服务
- 支持远程调用和批量处理
- 返回结构化的JSON格式结果

## 技术要点
- 文档解析和OCR技术
- 结构化数据提取
- HTTP服务发布和调用
- 文件上传和处理
- 异步任务执行
- JSON格式标准化输出
