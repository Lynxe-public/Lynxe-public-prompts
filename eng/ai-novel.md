# AI Novel

## Function Description

This is an example demonstrating how to use Function-Agent to implement long-form content creation, showing how to complete a full novel creation workflow through a divide-and-conquer strategy.

You can learn from this how to create multiple specialized function tools, how to implement function composition and calls, and how to coordinate the entire creation process through a main entry function.

## Usage Process

**Version Requirement**: 4.8.6 and above

**Step 1** Open the Lynxe system

**Step 2** Import data
- Import the plan template from the `prompt-script/ai_novel_demo.json` file
- The system will automatically identify and load all function Agents

**Step 3** Understand the function structure
- **Outline Writer**: Generates the novel outline and chapter structure based on theme and chapter count requirements
- **Chapter Content Writer**: Writes the specific chapter content based on theme and chapter name
- **Main Entry - Write Entire Novel**: Coordinates the entire creation process, first writing the outline, then writing the content for each chapter one by one

**Step 4** Execute the main entry function
- Run the "Main Entry - Write Entire Novel" function
- The system will automatically execute the following process:
  1. Call "Outline Writer" to generate article outline and chapter structure
  2. Read the outline content
  3. Call "Chapter Content Writer" one by one to write content for each chapter
- The final generated novel content is saved in the `article.md` file

**Step 5** View generation results
- Check the generated `article.md` file
- Verify chapter structure and content quality
- Confirm each chapter meets the word count requirement (1000 words)

## Expected Results

- Successfully import 3 function Agents: Outline Writer, Chapter Content Writer, and Main Entry function
- The system can automatically generate complete article outline and chapter structure based on theme
- Complete long-form content creation through divide-and-conquer approach
- Each chapter meets the specified word count requirement (1000 words)
- Article content has coherence and logic
- The final generated novel is saved in the `article.md` file

## Technical Points

- Function-Agent capability: Intelligent function composition and automatic task decomposition
- Function composition and reuse: Support for decomposing complex creation tasks into reusable tool functions
- Divide-and-conquer strategy: Decompose complex creation tasks into manageable chapter units
- File operations: Use global_file_operator tool for file read and write operations
- Recap mechanism: Maintain coherence between chapters through Recap.md file
- Word count control: Ensure each chapter meets the specified word count requirement
