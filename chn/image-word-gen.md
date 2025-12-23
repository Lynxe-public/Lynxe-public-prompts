# 图文生成与Word导出

<img width="1168" height="1288" alt="image" src="https://github.com/user-attachments/assets/5e977b03-395d-4c2d-b979-0590981aaea0" />

## 功能说明

这是一个展示如何生成带图片的Markdown内容并导出为Word文档的示例，演示了如何通过Function-Agent实现内容创作、图片生成和文档格式转换的完整流程。

你可以从这里了解如何创建包含图片的Markdown文档，如何使用AI生成图片，以及如何将Markdown文档转换为Word格式。

## 使用流程

**版本要求**: 4.9.2（含）以上 目前demo是基于通义的

**第1步** [打开Lynxe系统](https://github.com/spring-ai-alibaba/Lynxe)

**第2步** 导入数据
- 导入 [prompt-script/ImageWordGen.json](../prompt-script/ImageWordGen.json) 文件中的计划模板
- 系统会自动识别并加载函数Agent

**第3步** 理解函数功能
- **生成一个markdown带图内容并输出为word**: 这是一个集成函数，自动完成以下流程：
  1. 创作小说内容（约1000字，主题为人类被AI统治）
  2. 基于小说内容生成概念封面图片
  3. 将封面图片插入到Markdown文档中
  4. 将Markdown文档转换为Word格式

**第4步** 执行函数
- 运行"生成一个markdown带图内容并输出为word"函数

**第5步** 查看生成结果
- 检查生成的 `novel.md` 文件，确认内容质量和图片插入位置
- 查看生成的Word文档，验证格式转换效果
- 确认文档包含文字内容和封面图片

## 预期结果

- 成功生成约1000字的小说内容，主题为人类被AI统治
- 基于小说内容自动生成概念封面图片
- 封面图片正确插入到Markdown文档的标题下方
- Markdown文档成功转换为Word格式
- 生成的Word文档包含完整的文字内容和图片
- 所有文件保存在系统文件管理器中

## 技术要点

- Function-Agent能力：智能任务分解和自动化流程执行
- 内容创作：自动生成符合主题要求的长文本内容
- 图片生成：使用wan2.6-t2i模型进行AI图片生成
- 文件操作：使用file-operations_global_file_read_file_operator、file-operations_global_file_write_file_operator工具进行文件读写操作
- 格式转换：使用file-operations_markdown_to_docx工具将Markdown转换为Word文档
- 图片插入：自动将生成的图片插入到Markdown文档的指定位置
- 多步骤协调：通过单一函数调用完成多个步骤的自动化执行

