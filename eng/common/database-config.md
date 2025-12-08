# Database Configuration

## Function Description

The system has built-in database support capabilities, supporting both MySQL and local H2 databases.

With a database, it becomes more convenient to handle scenarios that require large-scale data processing. The database itself also supports efficient export to Excel, making it suitable as a core shared storage.

Additionally, since LLM can handle database and table creation logic more simply, as long as the database is properly configured, it works well as temporary structured storage for various scenarios.

## Configuration Steps

**Step 1** Open configuration in top right corner
- Click the configuration icon in the top right corner of the system

**Step 2** Click database configuration
- Select "Database Configuration" option in the configuration menu

**Step 3** Enter configuration information
- **Database Name**: Corresponds to the schema name in MySQL/H2
- **Type**: Select database type (MySQL or H2)
- **URL**: Socket address for database connection
- **Password**: Database access password

**Step 4** Test connection
- Click "Test Connection" button
- Confirm connection is successful

**Step 5** Save configuration
- After successful test, click "Save" button
- Configuration complete

## Expected Results

- Successfully configure database connection
- System can access database normally
- Support subsequent database operations (create tables, query, write, etc.)

## Technical Points

- Support for both MySQL and H2 database types
- Database as core shared storage
- Support for data export to Excel format
- LLM can automatically handle database and table creation logic
- Suitable as temporary structured storage for various scenarios

