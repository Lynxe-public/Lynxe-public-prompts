# Form Input Demo

## Introduction
Form-input is a process that allows the system to wait for user input information, which is a very common scenario. This example explains how to implement: first visit and log in to Zhihu, then let the system wait for the user to log in on Zhihu. After the user completes the login on Zhihu, click confirm in the system to continue with subsequent operations. Since the system can maintain the login state, there is no need to log in again next time.

## Func-Agent Enhanced Mode

### Description
This example uses enhanced func-agent to implement form input demo, demonstrating how to let the system wait for user interaction and maintain login state

### Specific Steps

**Step 1** Enter Func-Agent planning mode
- On the homepage, click the func-agent planning mode button in the bottom right corner of the system
- A new box "Func-agent plan template" will appear on the left

**Step 2** Create new plan
- Click "New Plan" button

**Step 3** Configure plan template
- Click "Add first step"
- Enter the following information in sequence:
  - **Plan template name**: `Login to Zhihu and output the first 3 contents of Zhihu homepage`
  - **Task requirements**:
    ```
    First open https://www.zhihu.com/ 
    Then output the first 3 questions and answers from Zhihu homepage, no need to click into specific answers, just return the information from the list.

    When you think Zhihu requires user login, use form_input tool
    Give user a checkbox: Already completed Zhihu login 
    Use this method to wait for user login before continuing
    ```
  - **Task output requirements**: `Empty`

**Step 4** Select tools
- Click "Add/Remove Tools" button
- Select the following tools:
  - `browser_use` tool
  - `form_input` tool

**Step 5** Save plan
- Click "save" button
- Wait for "Save successful" prompt

**Step 6** Execute plan
- Click "Execute Plan" button
- Observe the system opening browser and accessing Zhihu

**Step 7** User login interaction
- When Zhihu prompts for login, complete login on Zhihu website
- Return to system page
- System will display a dialog asking if login is completed
- Enter "ok" and click "Confirm"

**Step 8** View results
- System will return the first 3 contents of homepage based on logged-in Zhihu state
- Observe the questions and answers information output by the system

**Step 9** Verify login state persistence (optional)
- After the previous task is completed and correctly output
- Click "Execute Plan" button again
- System will directly output results based on logged-in Zhihu state
- No need to log in again

## Expected Results
- System successfully opens Zhihu website
- Uses form_input tool to wait for user to complete login
- After login, system can obtain Zhihu homepage content
- Login state is maintained, subsequent operations don't require re-login

## Technical Points
- Form-input tool usage methods
- User interaction waiting mechanism
- Browser session state maintenance
- Login state persistence
- Asynchronous user interaction handling

