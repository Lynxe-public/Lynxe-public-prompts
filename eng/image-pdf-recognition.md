# Image and PDF Recognition

## Function Description

This is an example that demonstrates PDF download and document parsing capabilities, showing how to download PDF documents from websites through browser automation technology and extract structured information using document parsing tools.

You can learn from this how to configure browser automation tools to implement web navigation and file downloading, and how to use document parsing tools to extract key information from documents.

This example demonstrates the use of dynamic agent mode (dynamic_agent), automatically completing web operations and file downloads through browser tools, then using document parsing tools to extract the required structured information.

## Usage Process

**Step 1** [Open the Lynxe system](https://github.com/spring-ai-alibaba/Lynxe)

**Step 2** Import data
- Import the plan template from the [prompt-script/download_and_analyze.json](../prompt-script/download_and_analyze.json) file
- The system will automatically identify and load the plan template, including browser automation tools and document parsing tool configurations

**Step 3** Execute plan
- Click "Execute Plan" button
- Observe the system automatically opening the browser, navigating to the website, downloading the PDF document, and parsing it
- View preliminary output results

**Step 4** Verify results
- Check if the system successfully downloaded the PDF document
- Confirm document parsing functionality works normally
- Verify if the fund cost section content was successfully extracted
- Check structured output format

## Expected Results
- Successfully build PDF download and parsing capabilities
- System can automatically download PDF documents from websites
- System can parse document content and extract key information (such as fund cost section)
- Support browser automation operations
- Return structured parsing results

## Technical Points
- Browser automation technology (navigation, clicking, downloading)
- Document parsing and conversion technology (markdown_converter)
- File system operations (reading, searching)
- Structured data extraction
- Dynamic agent mode (dynamic_agent)
