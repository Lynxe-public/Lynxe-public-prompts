# MCP Service Configuration

## Function Description

MCP (Model Context Protocol) services allow the system to extend functionality through external services. By configuring MCP services, external tools and services can be integrated into the system to achieve more powerful capabilities.

The system supports two connection methods: via stdio link or via SSE/Streaming link.

## Configuration Methods

### Via stdio Link

**Step 1** Obtain MCP service information
- Visit `https://modelscope.cn/mcp` to get MCP services
- Log in with your account
- Select the required MCP service and choose "stdio" method
- Copy the configuration information (JSON format)

**Step 2** Enter Lynxe MCP configuration page
- Click the configuration icon in the top right corner of the dialog box
- Select "Tools/MCP Configuration"

**Step 3** Import MCP configuration
- Click "Import All" button
- Paste the copied JSON configuration information into the input box
- Click "Import" button

**Step 4** Wait for configuration to complete
- Wait for the system to load the configuration information
- When "MCP Success" prompt appears, configuration is complete
- MCP service is ready to use

### Via SSE/Streaming Link

**Step 1** Enter MCP configuration page
- Click the configuration icon in the top right corner of the dialog box
- Select "Tools/MCP Configuration"
- Click "New MCP Configuration"

**Step 2** Obtain MCP service information
- Log in to the MCP service provider platform (e.g., `mcp.higress.ai`)
- Log in with the corresponding account (some platforms provide free quota)
- Search and select the required MCP service
- Open the service and copy the SSE URL
- **Note**: Only copy the URL part, not the JSON format, for example: `https://mcp.higress.ai/mcp-service/xxxxxxxxx/sse`

**Step 3** Configure MCP service
- Return to the system configuration page
- Enter the following information in the configuration box:
  - **MCP Name**: Set an easily recognizable name for the MCP service
  - **Connection Type**: Select `sse`
  - **URL**: Paste the SSE URL copied earlier
- Click "Save" button
- Wait for system confirmation
- Confirm that MCP service shows as "Enabled"

**Step 4** Use MCP service
- After configuration is complete, return to the main interface
- In Func-Agent planning mode, you can find the newly configured MCP service in the tool list
- Select the corresponding MCP tool and enable related functions
- Use MCP tools in plans to complete corresponding tasks
