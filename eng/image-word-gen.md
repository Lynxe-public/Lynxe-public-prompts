# Image and Word Generation

## Function Description

This is an example demonstrating how to generate Markdown content with images and export it as a Word document, showing how to implement a complete workflow of content creation, image generation, and document format conversion through Function-Agent.

You can learn from this how to create Markdown documents with images, how to use AI to generate images, and how to convert Markdown documents to Word format.

## Usage Process

**Version Requirement**: 4.9.2 and above (Currently demo is based on Tongyi)

**Step 1** [Open the Lynxe system](https://github.com/spring-ai-alibaba/Lynxe)

**Step 2** Import data
- Import the plan template from the [prompt-script/ImageWordGen.json](../prompt-script/ImageWordGen.json) file
- The system will automatically identify and load the function Agent

**Step 3** Understand the function
- **Generate a markdown with images and output as word**: This is an integrated function that automatically completes the following process:
  1. Create novel content (approximately 1000 words, theme: humans being ruled by AI)
  2. Generate a concept cover image based on the novel content
  3. Insert the cover image into the Markdown document
  4. Convert the Markdown document to Word format

**Step 4** Execute the function
- Run the "Generate a markdown with images and output as word" function

**Step 5** View generation results
- Check the generated `novel.md` file, confirm content quality and image insertion position
- View the generated Word document, verify format conversion effect
- Confirm the document contains text content and cover image

## Expected Results

- Successfully generate approximately 1000 words of novel content with the theme of humans being ruled by AI
- Automatically generate a concept cover image based on the novel content
- Cover image correctly inserted below the title in the Markdown document
- Markdown document successfully converted to Word format
- Generated Word document contains complete text content and images
- All files saved in the system file manager

## Technical Points

- Function-Agent capability: Intelligent task decomposition and automated workflow execution
- Content creation: Automatically generate long text content that meets theme requirements
- Image generation: Use wan2.6-t2i model for AI image generation
- File operations: Use file-operations_global_file_read_file_operator and file-operations_global_file_write_file_operator tools for file read and write operations
- Format conversion: Use file-operations_markdown_to_docx tool to convert Markdown to Word document
- Image insertion: Automatically insert generated images into specified positions in Markdown documents
- Multi-step coordination: Complete multiple steps of automated execution through a single function call

