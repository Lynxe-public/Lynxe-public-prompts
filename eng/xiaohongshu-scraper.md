# Xiaohongshu Search Scraping

## Function Description

This is an example that uses a browser to open Xiaohongshu, search for a keyword, then retrieves the top 10 pages and stores them in a database.

You can learn from this example how to use browser tools, database tools, and parallel execution tools.

## Usage Process

**Version Requirement**: 4.8.6 or higher

**Step 1** Open Lynxe system

**Step 2** Configure database
- Ensure database service is properly configured
- System supports H2 database
- For detailed configuration steps, please refer to: [Database Configuration](common/database-config.md)

**Step 3** Import data
- Import the plan templates from [prompt-script/xiaohongshu-scraper.json](prompt-script/xiaohongshu-scraper.json) file
- System will automatically recognize and load all steps

**Step 4** Execute initialization steps
- Run "Step 1: Login" and "Step 2: Create database table" in sequence
- These two steps only need to be executed once to complete login and create database table structure

**Step 5** Execute search scraping (can be run repeatedly)
- Run "Step 3: Get top 10 items from a specific category"
- Enter search keyword and category information
- System will automatically search, scrape and store data into database
- This step can be run repeatedly to scrape different search keywords

## Expected Results

- Successfully log in to Xiaohongshu website
- Create `crawl_data` database table with id, category, title, details fields
- Retrieve top 10 related content based on search keyword
- Store scraped content into database
- Support repeated execution of search and scraping tasks

## Technical Points

- Browser tool usage: Open web pages, search, retrieve content
- Database tool usage: Create tables, query data, write data
- Parallel execution tool usage: Process multiple link scraping tasks in parallel
- User interaction waiting: Handle login state
- File operations: Temporarily save web page content

