# Functional Agent

## Introduction
This example demonstrates how to use the system to complete a DeepResearch-type application, where answers are completely based on real information from all pages actually viewed, with clear citations. It also serves as a concrete demonstration of "functions as first-class citizens" by decomposing complex tasks into reusable tool functions.

## Func-Agent Enhanced Mode

### Description
This example uses enhanced func-agent to implement enhanced research search, demonstrating how to complete complex research tasks through function composition

### Specific Steps

#### Part 1: Publish a function to get detailed information from a single page

**Step 1** Enter Func-Agent planning mode
- On the homepage, click the func-agent planning mode button in the bottom right corner of the system
- A new box "Func-agent plan template" will appear on the left

**Step 2** Create new plan
- Click "New Plan" button

**Step 3** Configure plan template
- Click "Add first step"
- Enter the following information in sequence:
  - **Plan template name**: `Get current page information and answer questions`
  - **Task requirements**:
    ```
    First open <<Website URL>>
    Get its getText content.
    Then, from the content, get content related to user question: <<User Question>> and return, including all obtained facts and data.
    You only need to access the current page, no need to expand to access sub-pages.
    ```
  - **Task output requirements**: `User question, Answer to question, Key evidence`

**Step 4** Select tools
- Click "Add/Remove Tools" button
- Select `browser_use` tool

**Step 5** Save plan
- Click "save" button
- Wait for "Save successful" prompt

**Step 6** Publish as tool service
- Select "Publish as Tool Service"
- Fill in the following information in sequence:
  - **Tool Name**: `Get current page information and answer questions`
  - **Tool Description**: `This tool can rely on website URL and user questions to access the website to answer user questions`
  - **Service Group**: `Research Query`
  - **Parameter Configuration**:
    - `Website URL`: URL address of the website to be accessed, must be complete URL e.g. https:url.com/subhtml
    - `User Question`: Specific question to be answered based on the website
- Select "Publish as Internal Tool Call"
- Confirm successful publication

#### Part 2: Publish a method to get research URLs from Baidu

**Step 7** Create second plan
- On the homepage, click the func-agent planning mode button again
- Click "New Plan" button

**Step 8** Configure second plan template
- Click "Add first step"
- Enter the following information in sequence:
  - **Plan template name**: `Get research URL information from Baidu`
  - **Task requirements**:
    ```
    First open Baidu search engine
    Organize all links related to user question: <<User Question>>
    Get the first 5 related links from the first page of search results through getText method.

    Then use the "Get current page information and answer questions" tool to access each link to get answers.
    ```
  - **Task output requirements**: `User question, Answer to question, Key evidence`

**Step 9** Select tools
- Click "Add/Remove Tools" button
- Select the following tools:
  - `Get current page information and answer questions` tool (just created)
  - `browser_use` tool

**Step 10** Save and execute plan
- Click "save" button
- Select "Execute Plan"

## Expected Results
- Successfully publish two reusable tool functions
- First function can get detailed information from a single page and answer questions
- Second function can get related URLs from Baidu search and conduct deep research
- Implement complex research search functionality through function composition
- All answers are based on real content from actually accessed pages with clear citations

## Technical Points
- Functions as first-class citizens design philosophy
- Tool function publication and reuse
- Complex task decomposition and composition
- Deep research implementation methods
- Answer generation based on real data
- Clear presentation of citations and evidence

