# Function-Agent Example

## Function Description

**The core of Func-Agent is defining an Agent in the form of a function.** A Func-Agent can be described as four parts:

- **Function name**: Unique identifier for invocation and routing.
- **Structured parameter schema**: Inputs are described as JSON (e.g. param1, param2, param3), not free-form natural language.
- **Function body**: A textual description of the task to perform, executed by the Agent; the body may call other Func-Agents.
- **Structured return value**: Results are returned in JSON or similar form for downstream systems or other Agents.

For example, "Technical Expert Problem Handling" in this demo: the function name is that label; input might be `{"question": "How do I optimize this SQL?"}`; the body is described as "Answer the user's technical question with expertise" and is executed by the Agent; the return is structured answer content for the router or a ticket system.

In other words, the Agent gets a "function-style label" so it can be invoked in a structured, non–natural-language way, improving accuracy for system integration and Agent-to-Agent collaboration.

**Two direct benefits:** First, any existing system’s requests can be turned into JSON, so integration is straightforward. Second, with structured inputs and outputs, the information passed between Agents during collaboration is more precise, avoiding call errors caused by natural-language ambiguity.

This example shows how to build an intelligent problem classifier and expert system using function composition and routing. You will see how to create multiple specialized Agent functions, compose and call them, and route questions to the right expert via a routing Agent. The technical expert, database expert, and business expert here are three sub-agents with independent memory that can run in parallel—our recommended way to use sub-agents.

## Usage Process

**Version Requirement**: 4.8.6 and above

**Step 1** [Open the Lynxe system](https://github.com/spring-ai-alibaba/Lynxe)

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
