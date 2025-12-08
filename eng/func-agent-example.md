# Function-Agent Example

## Function Description

This is an example that demonstrates the Function-Agent design philosophy, showing how to implement intelligent problem classification and expert systems through function composition and routing mechanisms.

You can learn from this how to create multiple specialized Agent functions, how to implement function composition and calls, and how to route problems to appropriate experts through a routing Agent.

In this example, the technical expert, database expert, and business expert correspond to three sub-agents. They have completely independent memory resources and can be used in parallel. This is the best practice we have found for using sub-agents.

## Usage Process

**Version Requirement**: 4.8.6 and above

**Step 1** Open the Lynxe system

**Step 2** Import data
- Import the plan template from the [prompt-script/func-agent-example.json](../prompt-script/func-agent-example.json) file
- The system will automatically identify and load all function Agents

**Step 3** Understand the function structure
- **Technical Expert Problem Handling**: An Agent function specialized in handling technical problems
- **Database Expert Problem Handling**: An Agent function specialized in handling database problems
- **Business Expert Problem Handling**: An Agent function specialized in handling business problems
- **Main Entry - Routing Method**: The main entry function that automatically routes to the appropriate expert based on problem type. This is the core startup function, and you need to ensure it correctly references the other three func-agents. This should be automatic, but there may be issues with incorrect references being ignored due to version differences.

**Step 4** Execute the routing function
- Run the "Main Entry - Routing Method" function
- Input user requirements or problems
- The system will automatically determine the problem type and route to the corresponding expert function
- The expert function will return the corresponding answer after processing

## Expected Results

- Successfully import 4 function Agents: routing function and 3 expert functions
- The routing function can correctly identify problem types (technical/database/business)
- Problems are automatically routed to corresponding expert functions for processing
- Each expert function returns answers that match their professional domain
- Support function composition and reuse, embodying the "functions as first-class citizens" design philosophy

## Technical Points

- Function-Agent capability: Intelligent function composition and automatic task decomposition, which is also one of the most critical features of the entire system
- Function composition and reuse: Support for decomposing complex tasks into reusable tool functions
- Routing mechanism: Automatically select the most appropriate processing function based on problem type
- Function publishing: All functions can be called as independent tools
- Parameter passing: Support parameter passing and result return between functions
