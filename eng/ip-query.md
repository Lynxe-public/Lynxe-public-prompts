# IP Query

## Introduction
IP query is an example that demonstrates how MCP services can be integrated into the system. Through this case study, users can learn how to configure and use external MCP services to extend system functionality.

## Func-Agent Enhanced Mode

### Description
This example uses enhanced func-agent to implement IP query, demonstrating how to integrate MCP services into the system

### Specific Steps

**Step 1** Enter MCP configuration page
- Click the configuration icon in the top right corner of the dialog box
- Select "Tools/MCP Configuration"
- Click "New MCP Configuration"

**Step 2** Obtain MCP service information
- Log in to website `mcp.higress.ai`
- Use Alibaba Cloud account to log in (has free quota)
- Search for "IP Location" service
- Open the service and copy the SSE URL on the right
- Note: Only copy the URL part, not the JSON format, similar to: `"url": "https://mcp.higress.ai/mcp-ip-query/xxxxxxxxx/sse"`

**Step 3** Configure MCP service
- Return to the system configuration page
- Enter the following information in the configuration box:
  - **MCP Name**: `ip query`
  - **Connection Type**: `sse`
  - **URL**: Paste the SSE URL copied earlier
- Click "Save" button
- Wait for system confirmation
- Confirm that MCP service shows as "Enabled"

**Step 4** Return to main interface
- Click "Return to Homepage" button

**Step 5** Enter Func-Agent planning mode
- Click the func-agent planning mode button in the bottom right corner of the system
- A new box "Func-agent plan template" will appear on the left

**Step 6** Create new plan
- Click "New Plan" button

**Step 7** Configure plan template
- Click "Add first step"
- Enter the following information in sequence:
  - **Plan template name**: `Query local IP using IP query`
  - **Task requirements**: `Use IP query tool to query local IP`
  - **Task output requirements**: `Empty`

**Step 8** Select MCP tools
- Click "Add/Remove Tools" button
- Select "ip query" tool
- Enable all related functions

**Step 9** Save plan
- Click "save" button
- Wait for "Save successful" prompt

**Step 10** Execute plan
- Click "Execute Plan" button
- Observe the system querying local IP process

**Step 11** View execution details (optional)
- Click "Detailed Execution Plan" button
- View detailed execution steps
- Observe specific MCP tool call process

## Expected Results
- System successfully queries and displays local IP address
- Complete MCP service call process can be viewed through execution details
- Learn how to integrate and use external MCP services

## Technical Points
- MCP (Model Context Protocol) service integration
- SSE (Server-Sent Events) connection method
- External service configuration and management
- Tool invocation in Func-Agent mode
