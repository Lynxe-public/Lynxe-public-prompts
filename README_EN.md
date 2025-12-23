# Public Use Cases Collection

## Project Introduction

This project contains a collection of practical use cases that demonstrate the core functionality of the system, covering various application scenarios from basic queries to advanced automated workflows. Each use case provides detailed documentation in both Chinese and English to help users quickly understand and master the system's usage methods.

## Use Cases Overview

### ⭐ Highly Recommended Func-Agent

#### Bing Search Q&A
- **File Location**: [chn/bing-search.md](chn/bing-search.md) | [eng/bing-search.md](eng/bing-search.md)
- **Why Recommended**: This is one of the most frequently used tools, capable of quickly searching and answering various questions
- **Description**: Uses MCP service to integrate Bing search engine, implementing intelligent Q&A functionality based on search results
- **Key Features**:
  - MCP service configuration and integration
  - Direct use in conversation, simple and convenient operation
  - Intelligent Q&A based on search results
- **Use Cases**: Information search, intelligent Q&A, real-time information query

---

### Product Feature Introduction - Func-Agent

#### 1. Function-Agent Example
- **File Location**: [chn/func-agent-example.md](chn/func-agent-example.md) | [eng/func-agent-example.md](eng/func-agent-example.md)
- **Why Recommended**: This is a core example demonstrating the Function-Agent design philosophy, showing how to implement intelligent problem classification and expert systems through function composition and routing mechanisms
- **Description**: Demonstrates the Function-Agent design philosophy, showing how to implement intelligent problem classification and expert systems through function composition and routing mechanisms
- **Key Features**:
  - Function-Agent capability: Intelligent function composition and automatic task decomposition
  - Independent memory resources for sub-agents: Technical expert, database expert, and business expert have completely independent memory resources
  - Parallel usage capability: Multiple sub-agents can be used in parallel
  - Routing mechanism: Automatically select the most appropriate processing function based on problem type
  - Function publishing and reuse: All functions can be called as independent tools
- **Use Cases**: Intelligent problem classification, expert systems, function composition, task routing

#### 2. Form Input Demo
- **File Location**: [chn/form-input-demo.md](chn/form-input-demo.md) | [eng/form-input-demo.md](eng/form-input-demo.md)
- **Why Recommended**: Demonstrates user interaction waiting mechanisms and login state persistence functionality, a core example for handling website operations requiring user login
- **Description**: Demonstrates user interaction waiting mechanisms and login state persistence functionality
- **Key Features**:
  - Form-input tool usage
  - Asynchronous user interaction handling
  - Browser session state maintenance
- **Use Cases**: Website operations requiring user login, interactive workflows

#### 3. Image and PDF Recognition
- **File Location**: [chn/image-pdf-recognition.md](chn/image-pdf-recognition.md) | [eng/image-pdf-recognition.md](eng/image-pdf-recognition.md)
- **Why Recommended**: A core example demonstrating image and PDF recognition functionality, supporting batch recognition and structured output, as well as HTTP API calls
- **Description**: Demonstrates image and PDF recognition functionality, supporting batch recognition and structured output, as well as HTTP API calls
- **Key Features**:
  - Document parsing and OCR technology
  - Structured data extraction
  - HTTP service publishing and calling
  - File upload and batch processing
  - Asynchronous task execution
  - JSON format standardized output
- **Use Cases**: Document processing, content extraction, batch recognition, API services

#### 4. Long Content Output Demo
- **File Location**: [chn/ai-novel.md](chn/ai-novel.md) | [eng/ai-novel.md](eng/ai-novel.md)
- **Why Recommended**: A core example demonstrating integrated output of long-form content and function-agent implementation, completing long-form content creation through divide-and-conquer strategy, supporting batch production of long articles
- **Description**: Demonstrates integrated output of long-form content and function-agent implementation, completing long-form content creation through divide-and-conquer strategy, supporting batch production of long articles
- **Key Features**:
  - Integrated long-form content output: Breaking through context limitations to achieve coherent long-form content generation
  - Divide-and-conquer strategy: Decomposing complex creation tasks into manageable chapter units
  - Content coherence assurance: Ensuring logical consistency and style uniformity between chapters
- **Use Cases**: Content creation, creative writing, batch article production, long-form document generation

---

### 📋 Scenario-based Case Library

#### 1. Xiaohongshu Search Scraping
- **File Location**: [chn/xiaohongshu-scraper.md](chn/xiaohongshu-scraper.md) | [eng/xiaohongshu-scraper.md](eng/xiaohongshu-scraper.md)
- **Description**: Demonstrates how to use browser tools, database tools, and parallel execution tools to implement a complete workflow for website search scraping and data storage
- **Key Features**:
  - Browser automation: Open websites, search keywords, retrieve page content
  - Database operations: Create table structures, query and store data
  - Parallel processing: Scrape multiple links concurrently
  - User interaction waiting: Handle and maintain login state
  - Data deduplication: Automatically detect and update existing data
- **Use Cases**: Website data scraping, content collection, information monitoring, data storage

#### 2. Bing Search Q&A
- **File Location**: [chn/bing-search.md](chn/bing-search.md) | [eng/bing-search.md](eng/bing-search.md)
- **Description**: Demonstrates how to use MCP service to integrate Bing search engine, implementing intelligent Q&A functionality based on search results
- **Key Features**:
  - MCP service configuration and integration
  - Plan template import and management
  - Enable functional services in conversation
  - Intelligent Q&A based on search results
  - Func-agent design philosophy of precisely controlling tool quantity
- **Use Cases**: Information search, intelligent Q&A, real-time information query

#### 3. Image and Word Generation
- **File Location**: [chn/image-word-gen.md](chn/image-word-gen.md) | [eng/image-word-gen.md](eng/image-word-gen.md)
- **Description**: Demonstrates how to generate Markdown content with images and export it as a Word document, implementing a complete workflow of content creation, image generation, and document format conversion
- **Key Features**:
  - Content creation: Automatically generate long text content that meets theme requirements
  - Image generation: Use wan2.6-t2i model for AI image generation
  - Format conversion: Convert Markdown documents to Word format
  - Image insertion: Automatically insert generated images into specified positions in Markdown documents
  - Multi-step coordination: Complete multiple steps of automated execution through a single function call
- **Use Cases**: Content creation, document generation, image-text layout, format conversion

## Technical Architecture

### Core Components
- **Func-Agent Mode**: The system's main working mode, supporting complex task planning and execution
- **Tool Integration**: Built-in browser_use tools and external MCP service integration
- **Function Composition**: Support for decomposing complex tasks into reusable tool functions
- **State Management**: Support for browser session and login state persistence

## File Structure

```
public-usecase/
├── README.md                    # Project overview (Chinese)
├── README_EN.md                # Project overview (English)
├── chn/                        # Chinese version use case docs
│   ├── stock-price-query.md    # Stock Price Query
│   ├── form-input-demo.md     # Form Input Demo
│   ├── query-plan.md          # Functional Agent
│   ├── image-pdf-recognition.md # Image and PDF Recognition
│   ├── ai-novel.md           # AI Novel
│   ├── bing-search.md        # Bing Search Q&A
│   ├── func-agent-example.md # Function-Agent Example
│   └── xiaohongshu-scraper.md # Xiaohongshu Search Scraping
└── eng/                       # English version use case docs
    ├── stock-price-query.md   # Stock Price Query
    ├── form-input-demo.md    # Form Input Demo
    ├── query-plan.md         # Functional Agent
    ├── image-pdf-recognition.md # Image and PDF Recognition
    ├── ai-novel.md          # AI Novel
    ├── bing-search.md       # Bing Search Q&A
    ├── func-agent-example.md # Function-Agent Example
    ├── image-word-gen.md   # Image and Word Generation
    └── xiaohongshu-scraper.md # Xiaohongshu Search Scraping
```

## Contributing

Contributions of new use cases and improvements to existing documentation are welcome. Please ensure:
- Provide both Chinese and English versions
- Use clear step numbering
- Include expected results and technical points
- Maintain consistent documentation formatting

## License

This project uses an open source license. Please see the LICENSE file for specific information.

## Discussion

Click this link to join the DingTalk group for discussion: [dingtalk group](https://qr.dingtalk.com/action/joingroup?code=v1,k1,PBuFX00snERuKcnnG4YAPK52FOXwAkLYlulUUD9KiRo=&_dt_no_comment=1&origin=11)
