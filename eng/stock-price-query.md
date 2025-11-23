# Stock Price Query

## Introduction
Stock price query is a fundamental capability demonstration that showcases the system's default functionality and capabilities: the ability to use the system's built-in browser tools to retrieve stock query information.

## Simple Mode

### Description
Use the simplest chat interface to implement stock query

### Specific Steps
**Step 1** Enter query command in chat box
- Enter in chat box: `Use Baidu to query the latest stock price of Alibaba`
- Wait for system feedback

## Func-Agent Enhanced Mode

### Description
Use enhanced func-agent to implement stock query, with variable parameter support to query different types of stock information, demonstrating the system's variable parameter method (this is also the system's main recommended mode)

### Specific Steps

**Step 1** Enter Func-Agent planning mode
- Click the func-agent planning mode button in the bottom right corner of the system
- A new box "Func-agent plan template" will appear on the left

**Step 2** Create new plan
- Click the "New Plan" button

**Step 3** Configure plan template
- Click "Add first step"
- Enter the following information in sequence:
  - **Plan template name**: `Use Baidu to query any company's stock price`
  - **Task requirements**: `Use Baidu to query the latest stock price of <<Company Name>>`
  - **Task output requirements**: `Empty`

**Step 4** Select tools
- Click "Add/Remove Tools" button
- Find the `browser_use` tool (selecting precise tools helps AI improve task accuracy)

**Step 5** Save plan
- Click "save" button
- Wait for "Save successful" prompt

**Step 6** Fill in parameters
- Scroll down in the left plan template panel
- Find the newly appeared parameter "Company Name" that needs to be filled (this is the variable parameter)
- Enter a company name, such as "Alibaba" or other company names

**Step 7** Execute plan
- Click "Execute Plan" button
- Observe the plan execution process

**Step 8** View execution details (optional)
- Click on the currently executing task in the dialog box
- View detailed information for each round in the right panel:
  - Detailed input from system and large model
  - Output content
  - What functions were called
  - What results were returned

## Expected Results
- Simple mode: Display stock price information directly in the chat box
- Func-Agent mode: Flexibly query stock prices of different companies through variable parameters, and view the complete execution process in execution details

