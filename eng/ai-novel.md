# AI Novel

## Important Notes

**Version Requirement**: This use case requires system version 4.0.8 or higher to run properly. Please ensure your system version meets this requirement.

## Introduction
This example demonstrates how to use the system to complete long-form content generation. Long-form content generation is generally limited by the system's context word count. Therefore, we need to leverage the Agent's divide-and-conquer capabilities to complete it in segments. This example demonstrates how to complete coherent long-form content by decomposing complex long-form creation tasks into manageable chapters, achieving intelligent content generation.

## Func-Agent Enhanced Mode

### Description
This example uses enhanced func-agent to implement AI novel generation, demonstrating how to complete long-form content creation through divide-and-conquer approach

### Specific Steps

#### Part 1: Publish a tool to generate individual chapters

**Step 1** Enter Func-Agent planning mode
- On the homepage, click the func-agent planning mode button in the bottom right corner of the system
- A new box "Func-agent plan template" will appear on the left

**Step 2** Create new plan
- Click "New Plan" button

**Step 3** Configure plan template
- Click "Add first step"
- Enter the following information in sequence:
  - **Plan template name**: `Generate individual chapter information`
  - **Task requirements**:
    ```
    Based on the overall article chapter outline: <<Article Outline>> 
    Generate the specific chapter of the current article: <<Current Chapter Name>>
    Target article file address: <<Document Address>>
    Generation method:
    First need to read the entire document. 
    Then write the current chapter that needs to be completed 
    Word count requirement: <<Word Count Requirement>>
    ```
  - **Task output requirements**:
    ```
    Current chapter name, completion status (completed/incomplete), word count
    ```

**Step 4** Select tools
- Click "Add/Remove Tools" button
- Select `global_file_operator` tool

**Step 5** Save plan
- Click "save" button
- Wait for "Save successful" prompt

**Step 6** Publish as tool service
- Scroll down and select "Publish as Service"
- Fill in the following information in sequence:
  - **Tool Name**: `Tool for writing individual chapters`
  - **Tool Description**: `Tool that can write individual novel chapters`
  - **Service Group**: `Article Generation`
  - **Parameter Configuration**:
    - `Article Outline`: Overall outline of the entire article
    - `Current Chapter Name`: Chapter name that needs to be completed in the current task based on the overall outline, chapter name must appear in the outline
    - `Document Address`: Address of the target document for final output
    - `Word Count Requirement`: Word count requirement for each chapter
- Select "Publish as Internal Tool Call"

#### Part 2: Build AI Earth Domination Article Generation Template

**Step 7** Create second plan
- On the homepage, click the func-agent planning mode button again
- Click "New Plan" button

**Step 8** Configure second plan template
- Click "Add first step"
- Enter the following information in sequence:
  - **Plan template name**: `Generate an article about AI ruling Earth`
  - **Task requirements**:
    ```
    Build an article about AI ruling Earth.
    First, need to build a title and a set of chapters, requiring 5 chapters, mainly about how AI step by step rules Earth. Write the title and chapter names into ai-novel.md. Each chapter 1000 words
    Then, call the tool for writing individual chapters, one chapter at a time, to complete the entire article
    ```
  - **Task output requirements**:
    ```
    Novel file name, completion status
    ```

**Step 9** Select tools
- Click "Add/Remove Tools" button
- Select the following tools:
  - `global_file_operator` tool
  - `Tool for writing individual chapters` (just created)

**Step 10** Save and execute plan
- Click "save" button
- Click "Execute Plan" button
- Observe the system's process of generating article outline and chapters

**Step 11** View generation results
- Check the generated `ai-novel.md` file
- Verify chapter structure and content quality
- Confirm each chapter meets the word count requirement

**Step 12** Extend functionality (optional)
- Can later extend to include content writing based on chapters, then illustration and other logic for completing long-form content
- Welcome to try more creative functions

## Expected Results
- Successfully publish chapter generation tool
- System can generate complete article outline and chapter structure
- Complete long-form content creation through divide-and-conquer approach
- Each chapter meets the specified word count requirement
- Article content has coherence and logic

## Technical Points
- Divide-and-conquer creation strategy
- Tool function publication and reuse
- Structured management of long-form content
- Chapter-based writing workflow
- Content coherence assurance
- Word count control and quality management

## Extension Suggestions
- Can add illustration functionality
- Support multiple writing styles and genres
- Implement content quality assessment
- Add collaborative editing features
- Support multi-language creation

