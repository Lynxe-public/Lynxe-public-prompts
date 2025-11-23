# Image and PDF Recognition

## Introduction
Image and PDF recognition is a very common functional requirement for AI Agents. This system supports batch recognition of images and PDFs with structured output according to requirements, and also supports using image recognition through API calls. Through this use case, users can learn how to build document parsing capabilities and publish them as reusable services.

## Func-Agent Enhanced Mode

### Description
This example uses enhanced func-agent to implement image and PDF recognition functionality, demonstrating how to build structured document parsing capabilities and publish them as HTTP services

### Specific Steps

#### Part 1: Build Structured PDF/Image Parsing Capabilities

**Step 1** Enter Func-Agent planning mode
- On the homepage, click the func-agent planning mode button in the bottom right corner of the system
- A new box "Func-agent plan template" will appear on the left

**Step 2** Create new plan
- Click "New Plan" button

**Step 3** Configure plan template
- Click "Add first step"
- Enter the following information in sequence:
  - **Plan template name**: `Recognize PDF files based on images`
  - **Task requirements**:
    ```
    Based on uploaded PDF/jpeg files, answer the following key questions:
    What are the first 100 characters and the last 100 characters of this file respectively (you can change to your own analysis requirements)
    ```
  - **Task output requirements**: `Position (front/back), detailed content`

**Step 4** Select tools
- Click "Add/Remove Tools" button
- Select the following tools:
  - `markdown_converter` tool
  - `global_file_operator` tool

**Step 5** Save plan
- Click "save" button
- Wait for "Save successful" prompt

**Step 6** Upload files
- Click "Attach Files" button
- Select an image file or PDF file that requires OCR capabilities
- Confirm successful file upload

**Step 7** Execute plan
- Click "Execute Plan" button
- Observe the system's process of recognizing and parsing the file
- View preliminary output results

#### Part 2: Publish as HTTP Service and Implement Remote Calls

**Step 8** Publish as tool service
- Click "Publish as Tool Service" at the bottom of the left sidebar
- Fill in the following information in sequence:
  - **Tool Name**: `pdf_recognizer`
  - **Tool Description**: `Can be used for automatic PDF recognition`
  - **Service Group**: `document-reader` (can be replaced with a convenient management name)
- Select "Publish as Internal Tool Call" and "Publish as HTTP Service"
- Click "Publish as Service"

**Step 9** View call examples
- System will display examples of multiple calling methods
- Provides get+sync, post+sync, post+async calling methods
- Recommend using post+sync for debugging

**Step 10** File upload call
- Use POST method to upload files:
  ```bash
  curl -X POST \
    -F "files=@/path/to/your/file.pdf" \
    http://localhost:18080/api/file-upload/upload
  ```
- Expected return result:
  ```json
  {
    "success": true,
    "message": "Files uploaded successfully",
    "uploadKey": "upload-1760933409277_77_50",
    "uploadedFiles": [
      {
        "originalName": "your/file.pdf",
        "size": 262219,
        "type": "application/pdf",
        "uploadTime": [2025,10,20,12,10,9,278841000],
        "success": true
      }
    ]
  }
  ```

**Step 11** Execute recognition task
- Use uploadKey as parameter, call post+async method:
  ```bash
  POST /api/executor/executeByToolNameSync
  Content-Type: application/json
  
  {
    "toolName": "pdf_recognizer",
    "replacementParams": {
      "rawParam": "test"
    },
    "uploadedFiles": ["upload-1760933409277_77_50"]
  }
  ```
- **Note**: `"upload-1760933409277_77_50"` is an example uploadKey value returned from the previous step. In actual calls, replace it with the real uploadKey value returned from Step 10
- **Parameter Note**: The `"rawParam": "test"` in `replacementParams` is only for demonstration purposes. Passing this value has no actual meaning. If the system requires parameters to be passed, you can use this method to pass them
- Expected return result:
  ```json
  {
    "status": "completed",
    "result": "Execution result here"
  }
  ```

**Step 12** Verify results
- Check the returned JSON standardized results
- Confirm document parsing functionality works normally
- Verify structured output format

## Expected Results
- Successfully build PDF/image recognition capabilities
- System can parse document content and extract key information
- Publish as reusable HTTP service
- Support remote calls and batch processing
- Return structured JSON format results

## Technical Points
- Document parsing and OCR technology
- Structured data extraction
- HTTP service publishing and calling
- File upload and processing
- Asynchronous task execution
- JSON format standardized output
