# Translation and Grammar Correction

## Function Description

This is an intelligent translation and grammar correction tool that supports translating Chinese to English and automatically correcting English grammar and spelling errors. The tool provides detailed grammar explanations and suggestions for more natural English expressions to help users improve their English language skills.

This feature can be used directly in the chat dialog, making it simple and convenient to use.

## Usage Process

**Step 1** [Open Lynxe system](https://github.com/spring-ai-alibaba/Lynxe)

**Step 2** Import plan template
- Import the plan template content from [prompt-script/translation-grammar.json](../prompt-script/translation-grammar.json) file
- The system will automatically recognize and load the template configuration

**Step 3** Update service status
- Open the plan template you just imported
- Select "Update service status"
- Enable the "Enable in conversation" option

**Step 4** Use in dialog
- Select "翻译并纠正我的语法错误" (Translate and correct my grammar errors) from the dropdown menu in the chat dialog
- Enter the content you want to translate or correct (Chinese or English)
- The system will automatically identify the input language:
  - If it's English, it will correct grammar and spelling errors and provide detailed grammar explanations
  - If it's Chinese, it will translate to English and provide grammar explanations and natural expression suggestions
