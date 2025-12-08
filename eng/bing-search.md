# Bing Search Q&A

## Function Description

This is an example that uses MCP service to open Bing search engine, search for key content, and answer user questions based on search results.

This feature can be used directly in the chat dialog, making it simple and convenient to use.

## Usage Process

**Step 1** [Open Lynxe system](https://github.com/spring-ai-alibaba/Lynxe)

**Step 2** Import MCP service
- Visit `https://modelscope.cn/mcp/servers/rainerWJY/bing-cn-mcp-enhanced`
- Find the "stdio" option on the right side of the page and copy the configuration information
- Follow the instructions in [MCP Service Configuration](common/mcp-config.md) to import the configuration information into Lynxe's MCP configuration

**Step 3** Import plan template
- Import the plan template content from [prompt-script/search_rag.json](../prompt-script/search_rag.json) file
- The system will automatically recognize and load the template configuration

**Step 4** Update service status
- Open the plan template you just imported
- Select "Update service status"
- Enable the "Enable in conversation" option

**Step 5** Use in dialog
- Select "Use Bing search to quickly answer questions" from the dropdown menu in the chat dialog
- Simply enter your question
- The system will automatically search and answer questions based on the results

## Expected Results

- Successfully configure Bing search MCP service
- Search functionality can be used directly in the dialog
- The system can automatically search for relevant content based on questions and provide answers

## Technical Points

- MCP service configuration and usage
- Plan template import and management
- Enable functional services in conversation
- Intelligent Q&A based on search results

## Follow-up Notes

This example well demonstrates a core design philosophy of func-agent: **The best way to make models use tools better is to precisely control the number of tools each func-agent can use**. By limiting the scope of available tools, we can ensure that models complete tasks more focused and accurately.
