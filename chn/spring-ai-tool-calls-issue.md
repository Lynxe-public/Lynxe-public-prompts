# Spring AI 工具调用格式错误问题解决方案

## 问题描述

在使用 Spring AI 进行工具调用时，可能会遇到以下格式错误：

### 错误现象

返回的 `toolCalls` 数组中存在以下问题：

1. **重复的工具调用 ID**：两个条目使用相同的 `id`
2. **不完整的字段**：
   - 第一个条目：有 `name` 但 `arguments` 为空字符串
   - 第二个条目：`name` 为空字符串，但 `arguments` 有值

**错误示例：**
```json
"toolCalls": [
    {
        "id": "call_55b3d0a08a9c4f05bd0bcc",
        "type": "function",
        "name": "browser-service-group_navigate-browser",
        "arguments": ""
    },
    {
        "id": "call_55b3d0a08a9c4f05bd0bcc",
        "type": "function",
        "name": "",
        "arguments": "{\"url\": \"https://www.xiaohongshu.com/explore\"}"
    }
]
```

**正确格式应该是：**
```json
"toolCalls": [
    {
        "id": "call_55b3d0a08a9c4f05bd0bcc",
        "type": "function",
        "name": "browser-service-group_navigate-browser",
        "arguments": "{\"url\": \"https://www.xiaohongshu.com/explore\"}"
    }
]
```

### 详细错误场景

#### 场景 1：流式响应处理中的分块数据问题

**触发条件：**
- 使用 `ChatClient.stream()` 方法进行流式调用
- 模型返回的工具调用信息被拆分为多个数据块（chunks）
- 每个数据块可能只包含部分字段（如只有 `id` 和 `name`，或只有 `id` 和 `arguments`）

**错误表现：**
- 在流式处理过程中，同一个工具调用的 `name` 和 `arguments` 可能在不同的数据块中到达
- 如果框架在处理每个数据块时都创建新的 `ToolCall` 对象，就会导致重复的 ID 和不完整的字段

**可能的源码位置：**
- `org.springframework.ai.chat.client.ChatClient` 的流式响应处理逻辑
- `org.springframework.ai.chat.model.ChatResponse` 的构建过程
- `org.springframework.ai.chat.model.StreamingChatModel` 的实现类
- 各模型提供商的适配器（如 `OpenAiChatModel`、`QwenChatModel` 等）中的流式响应解析

**关键类和方法（推测）：**
- `ChatResponse.Builder` - 构建 ChatResponse 对象
- `ToolCall` 或 `FunctionCall` - 工具调用的数据结构
- `StreamingResponseHandler` - 处理流式响应的接口
- `AbstractChatModel.stream()` - 抽象流式调用方法

#### 场景 2：工具调用解析器的重复解析

**触发条件：**
- 在流式响应中，同一个工具调用可能被多次解析
- 解析器在处理不完整数据时创建了多个 `ToolCall` 对象

**错误表现：**
- 同一个 `id` 出现多次
- 每次解析时只填充部分字段

**可能的源码位置：**
- `org.springframework.ai.chat.client.advisor.ToolCallingManager` 或 `DefaultToolCallingManager`
- `org.springframework.ai.chat.model.ChatResponse` 的 `getResult().getOutput().getToolCalls()` 方法
- 各模型提供商的响应解析器（Response Parser）

**关键类和方法（推测）：**
- `ToolCallingManager.parseToolCalls()` - 解析工具调用
- `ChatResponse.getToolCalls()` - 获取工具调用列表
- `FunctionCall` 或 `ToolCall` 的构建器模式

#### 场景 3：JSON 反序列化时的字段映射错误

**触发条件：**
- 模型返回的 JSON 格式不标准
- Jackson 或其他 JSON 库在反序列化时出现问题
- 字段映射配置错误

**错误表现：**
- `name` 和 `arguments` 字段被错误地映射到不同的对象实例
- 空字符串被当作有效值处理

**可能的源码位置：**
- JSON 反序列化配置（Jackson ObjectMapper）
- `ToolCall` 或 `FunctionCall` 的注解配置（如 `@JsonProperty`）
- 响应 DTO 类的定义

**关键类和方法（推测）：**
- `ObjectMapper.readValue()` - JSON 反序列化
- `ToolCall` 类的字段注解和构造函数
- 响应解析器的 `parse()` 方法

### 调试建议

#### 1. 检查流式响应的原始数据

在源码中查找以下位置，添加日志输出：

```java
// 在流式响应处理的地方添加日志
chatClient.stream()
    .call(message)
    .doOnNext(chunk -> {
        // 打印每个数据块的原始内容
        System.out.println("Chunk: " + chunk);
        // 检查 toolCalls 的状态
        if (chunk.getResult().getOutput().getToolCalls() != null) {
            System.out.println("ToolCalls in chunk: " + 
                chunk.getResult().getOutput().getToolCalls());
        }
    })
    .collectList()
    .block();
```

**需要查找的源码位置：**
- `ChatClient` 实现类中的流式调用方法
- `StreamingChatModel` 的实现类
- 响应适配器（Response Adapter）中的数据处理逻辑

#### 2. 检查工具调用的合并逻辑

查找是否有合并相同 ID 工具调用的逻辑：

```java
// 在 ChatResponse.Builder 或类似的地方查找
List<ToolCall> toolCalls = response.getToolCalls();
Map<String, ToolCall> mergedCalls = new HashMap<>();
for (ToolCall call : toolCalls) {
    // 检查是否有合并逻辑
}
```

**需要查找的源码位置：**
- `ChatResponse.Builder` 类
- `DefaultToolCallingManager` 类
- 响应构建器（Response Builder）的实现

#### 3. 检查 ID 验证逻辑

查找是否有对空 ID 的验证：

```java
// 查找类似这样的验证逻辑
if (StringUtils.hasText(toolCall.getId())) {
    // 处理逻辑
}
```

**需要查找的源码位置：**
- `ToolCall` 或 `FunctionCall` 的构造函数
- 工具调用解析器的验证逻辑
- `ToolCallingManager` 的实现类

#### 4. 检查模型适配器的响应解析

不同模型提供商可能有不同的响应格式，检查对应的适配器：

**可能的源码位置：**
- `org.springframework.ai.openai` 包下的响应解析器
- `org.springframework.ai.anthropic` 包下的响应解析器
- `org.springframework.ai.qwen` 包下的响应解析器（如果使用通义千问）
- 其他模型提供商的适配器实现

**关键查找点：**
- `*ChatModel` 类的 `stream()` 方法实现
- `*Response` 类的解析逻辑
- `*StreamingResponseHandler` 的实现

### 源码查询指南

#### 在 Spring AI 源码中查找的关键路径：

1. **工具调用相关类：**
   ```
   org.springframework.ai.chat.model.ChatResponse
   org.springframework.ai.chat.model.ToolCall / FunctionCall
   org.springframework.ai.chat.client.advisor.ToolCallingManager
   org.springframework.ai.chat.client.advisor.DefaultToolCallingManager
   ```

2. **流式处理相关类：**
   ```
   org.springframework.ai.chat.client.ChatClient
   org.springframework.ai.chat.model.StreamingChatModel
   org.springframework.ai.chat.model.ChatResponse.Builder
   ```

3. **模型适配器：**
   ```
   org.springframework.ai.openai.OpenAiChatModel
   org.springframework.ai.anthropic.AnthropicChatModel
   org.springframework.ai.qwen.QwenChatModel
   ```

4. **响应解析器：**
   ```
   org.springframework.ai.*.api.*Response
   org.springframework.ai.*.client.*StreamingResponseHandler
   ```

#### 使用 GitHub 搜索的技巧：

1. 搜索关键词：
   - `toolCalls` + `duplicate`
   - `ToolCall` + `stream`
   - `parseToolCalls`
   - `ChatResponse` + `Builder`
   - `FunctionCall` + `merge`

2. 在 Spring AI 仓库中搜索：
   - Repository: `spring-projects/spring-ai`
   - 搜索 Issues 和 Pull Requests
   - 查看相关的讨论和修复记录

3. 检查版本差异：
   - 不同版本的 Spring AI 可能有不同的实现
   - 检查是否有相关的 bug fix 或改进

## 问题原因分析

### 1. 流式输出处理错误

在使用响应式编程模型（如 Flux）进行工具调用时，框架在处理模型返回的分块数据时，可能错误地将工具调用拆分成多个不完整的条目。

**常见错误**：
- 框架可能错误地将 ID 为空字符串的情况视为有效 ID
- 流式处理时，工具名称和参数可能在不同时间点到达，导致解析错误

**深层原因分析：**

#### 1.1 流式响应分块处理机制

在流式处理中，AI 模型的响应通常以数据块（chunks）的形式逐步返回。每个数据块可能包含：
- 第一个块：`{"id": "call_xxx", "name": "function_name"}`
- 第二个块：`{"id": "call_xxx", "arguments": "{...}"}`

**问题根源：**
- 如果框架在处理每个数据块时都创建新的 `ToolCall` 对象，而不是更新已存在的对象
- 如果缺少基于 `id` 的去重和合并逻辑
- 如果流式处理器的状态管理不当

**需要检查的源码位置：**
- `StreamingChatModel` 的实现类中的 `stream()` 方法
- `StreamingResponseHandler` 的实现，特别是 `onChunk()` 或类似方法
- `ChatResponse.Builder` 中处理流式数据块的逻辑
- 各模型提供商适配器中的流式响应解析器

**可能的代码模式：**
```java
// 错误模式：每次都创建新对象
public void onChunk(Chunk chunk) {
    ToolCall toolCall = new ToolCall();
    toolCall.setId(chunk.getId());
    toolCall.setName(chunk.getName()); // 可能为空
    responseBuilder.addToolCall(toolCall); // 导致重复
}

// 正确模式：基于 ID 合并
public void onChunk(Chunk chunk) {
    ToolCall existing = toolCallMap.get(chunk.getId());
    if (existing == null) {
        existing = new ToolCall();
        existing.setId(chunk.getId());
        toolCallMap.put(chunk.getId(), existing);
    }
    // 合并字段
    if (chunk.getName() != null) existing.setName(chunk.getName());
    if (chunk.getArguments() != null) existing.setArguments(chunk.getArguments());
}
```

#### 1.2 工具调用状态管理缺失

**问题：**
- 流式处理过程中，没有维护工具调用的中间状态
- 每个数据块都被当作独立的工具调用处理
- 缺少状态机来跟踪工具调用的完整性

**需要检查的源码位置：**
- `ToolCallingManager` 的实现类
- `ChatResponse.Builder` 的内部状态管理
- 流式响应处理器的状态维护逻辑

### 2. JSON 序列化/反序列化问题

在工具调用过程中，可能存在 JSON 序列化或反序列化的问题，导致格式错误。

**深层原因分析：**

#### 2.1 Jackson 反序列化配置问题

**可能的问题：**
- `@JsonIgnoreProperties(ignoreUnknown = true)` 配置导致字段丢失
- `@JsonProperty` 注解配置错误
- 自定义反序列化器（`JsonDeserializer`）处理不当

**需要检查的源码位置：**
- `ToolCall` 或 `FunctionCall` 类的注解配置
- `ObjectMapper` 的配置（可能在 `*ChatModel` 的配置类中）
- 自定义的 JSON 反序列化器实现

**检查点：**
```java
// 检查 ToolCall 类的定义
public class ToolCall {
    @JsonProperty("id")
    private String id;
    
    @JsonProperty("name")
    private String name; // 检查是否有默认值或验证
    
    @JsonProperty("arguments")
    private String arguments; // 检查类型是否正确
}
```

#### 2.2 响应格式不匹配

**问题：**
- 模型返回的 JSON 格式与预期的 DTO 结构不完全匹配
- 字段名称不一致（如 `function_call` vs `tool_call`）
- 嵌套结构处理错误

**需要检查的源码位置：**
- 各模型提供商的响应 DTO 类（如 `OpenAiChatResponse`、`QwenChatResponse`）
- 响应适配器（Response Adapter）中的映射逻辑
- API 客户端中的响应解析代码

### 3. 模型输出格式不规范

模型生成的工具调用格式可能不符合预期，导致解析错误。

**深层原因分析：**

#### 3.1 模型响应格式差异

不同模型提供商可能有不同的工具调用格式：

**OpenAI 格式：**
```json
{
  "tool_calls": [{
    "id": "call_xxx",
    "type": "function",
    "function": {
      "name": "function_name",
      "arguments": "{...}"
    }
  }]
}
```

**Anthropic 格式：**
```json
{
  "content": [{
    "type": "tool_use",
    "id": "toolu_xxx",
    "name": "function_name",
    "input": {...}
  }]
}
```

**问题：**
- 如果适配器没有正确处理不同格式的差异
- 如果格式转换逻辑有 bug
- 如果字段映射错误

**需要检查的源码位置：**
- 各模型提供商的响应解析器
- 格式转换器（Format Converter）
- 统一响应格式的适配器层

#### 3.2 流式响应中的不完整数据

**问题：**
- 模型在流式响应中可能先发送部分字段
- 解析器可能在数据不完整时就创建了 `ToolCall` 对象
- 后续的数据块没有正确更新已存在的对象

**需要检查的源码位置：**
- 流式响应解析器的增量更新逻辑
- `ChatResponse.Builder` 的增量构建逻辑
- 工具调用对象的更新机制

### 4. 工具调用解析器的实现缺陷

**可能的问题：**

#### 4.1 缺少去重逻辑

**问题：**
- 解析器没有检查 `id` 是否已存在
- 直接添加到列表中，导致重复

**需要检查的源码位置：**
- `ToolCallingManager.parseToolCalls()` 方法
- `ChatResponse.Builder.addToolCall()` 方法
- 工具调用列表的管理逻辑

#### 4.2 字段验证不足

**问题：**
- 没有验证 `id`、`name`、`arguments` 的完整性
- 允许空字符串作为有效值
- 缺少必填字段的检查

**需要检查的源码位置：**
- `ToolCall` 的构造函数或构建器
- 工具调用解析器的验证逻辑
- `ToolCallingManager` 的验证方法

#### 4.3 合并逻辑缺失

**问题：**
- 没有实现基于 `id` 的合并逻辑
- 多个不完整的 `ToolCall` 对象没有被合并

**需要检查的源码位置：**
- `ToolCallingManager` 的实现类
- `ChatResponse.Builder` 的合并逻辑
- 工具调用列表的去重和合并方法

## 解决方案

### 方案 1：工具调用解析时的合并和校验

在解析 `toolCalls` 时，检查是否存在相同 ID 的多个条目，并合并 `name` 和 `arguments`。

**实现思路：**
```java
// Pseudo code
Map<String, ToolCall> toolCallMap = new HashMap<>();
for (ToolCall call : toolCalls) {
    String id = call.getId();
    if (toolCallMap.containsKey(id)) {
        ToolCall existing = toolCallMap.get(id);
        // Merge name and arguments
        if (existing.getName().isEmpty() && !call.getName().isEmpty()) {
            existing.setName(call.getName());
        }
        if (existing.getArguments().isEmpty() && !call.getArguments().isEmpty()) {
            existing.setArguments(call.getArguments());
        }
    } else {
        toolCallMap.put(id, call);
    }
}
```

**源码级别的修复建议：**

#### 1.1 在 ChatResponse.Builder 中添加合并逻辑

**需要修改的位置：**
- `org.springframework.ai.chat.model.ChatResponse.Builder` 类
- `addToolCall()` 或类似方法

**修复代码示例：**
```java
public class ChatResponse {
    public static class Builder {
        private Map<String, ToolCall> toolCallMap = new HashMap<>();
        
        public Builder addToolCall(ToolCall toolCall) {
            String id = toolCall.getId();
            if (id == null || id.isEmpty()) {
                // 跳过无效的 tool call
                return this;
            }
            
            ToolCall existing = toolCallMap.get(id);
            if (existing != null) {
                // 合并字段
                if ((existing.getName() == null || existing.getName().isEmpty()) 
                    && toolCall.getName() != null && !toolCall.getName().isEmpty()) {
                    existing.setName(toolCall.getName());
                }
                if ((existing.getArguments() == null || existing.getArguments().isEmpty()) 
                    && toolCall.getArguments() != null && !toolCall.getArguments().isEmpty()) {
                    existing.setArguments(toolCall.getArguments());
                }
            } else {
                toolCallMap.put(id, toolCall);
            }
            return this;
        }
        
        public ChatResponse build() {
            // 将 Map 转换为 List
            List<ToolCall> toolCalls = new ArrayList<>(toolCallMap.values());
            // 验证完整性
            toolCalls.removeIf(call -> 
                call.getName() == null || call.getName().isEmpty() 
                || call.getArguments() == null || call.getArguments().isEmpty()
            );
            // ... 构建 ChatResponse
        }
    }
}
```

#### 1.2 在流式响应处理器中添加状态管理

**需要修改的位置：**
- `StreamingResponseHandler` 的实现类
- 流式响应处理器的 `onChunk()` 方法

**修复代码示例：**
```java
public class StreamingResponseHandler {
    private Map<String, ToolCall> toolCallState = new HashMap<>();
    
    public void onChunk(Chunk chunk) {
        if (chunk.getToolCalls() != null) {
            for (ToolCall chunkCall : chunk.getToolCalls()) {
                String id = chunkCall.getId();
                if (id == null || id.isEmpty()) {
                    continue; // 跳过无效的 tool call
                }
                
                ToolCall existing = toolCallState.get(id);
                if (existing == null) {
                    existing = new ToolCall();
                    existing.setId(id);
                    toolCallState.put(id, existing);
                }
                
                // 合并字段（只更新非空字段）
                if (chunkCall.getName() != null && !chunkCall.getName().isEmpty()) {
                    existing.setName(chunkCall.getName());
                }
                if (chunkCall.getArguments() != null && !chunkCall.getArguments().isEmpty()) {
                    existing.setArguments(chunkCall.getArguments());
                }
            }
        }
    }
    
    public List<ToolCall> getCompleteToolCalls() {
        // 返回完整的 tool calls
        return toolCallState.values().stream()
            .filter(call -> 
                call.getName() != null && !call.getName().isEmpty()
                && call.getArguments() != null && !call.getArguments().isEmpty()
            )
            .collect(Collectors.toList());
    }
}
```

### 方案 2：配置 ToolCallingManager

Spring AI 提供了 `ToolCallingManager` 接口来管理工具执行的生命周期。确保正确配置工具调用管理器。

**配置示例：**
```java
@Bean
ToolCallingManager toolCallingManager() {
    return ToolCallingManager.builder()
        .build();
}
```

或者提供自定义的 `ToolCallingManager` bean 来定制工具执行行为：

```java
@Bean
ToolCallingManager customToolCallingManager() {
    return new CustomToolCallingManager() {
        @Override
        public List<ToolCall> parseToolCalls(String response) {
            // Custom parsing logic with merge and validation
            List<ToolCall> calls = super.parseToolCalls(response);
            return mergeDuplicateToolCalls(calls);
        }
    };
}
```

**源码级别的修复建议：**

#### 2.1 自定义 ToolCallingManager 实现

**需要查找的源码位置：**
- `org.springframework.ai.chat.client.advisor.ToolCallingManager` 接口
- `org.springframework.ai.chat.client.advisor.DefaultToolCallingManager` 实现类

**自定义实现示例：**
```java
@Component
public class MergingToolCallingManager implements ToolCallingManager {
    
    @Override
    public List<ToolCall> parseToolCalls(ChatResponse response) {
        List<ToolCall> rawCalls = response.getResult().getOutput().getToolCalls();
        if (rawCalls == null || rawCalls.isEmpty()) {
            return Collections.emptyList();
        }
        
        // 合并相同 ID 的 tool calls
        Map<String, ToolCall> mergedCalls = new LinkedHashMap<>();
        for (ToolCall call : rawCalls) {
            String id = call.getId();
            if (id == null || id.isEmpty()) {
                // 记录警告日志
                log.warn("Skipping tool call with empty ID: {}", call);
                continue;
            }
            
            ToolCall existing = mergedCalls.get(id);
            if (existing != null) {
                // 合并字段
                mergeToolCall(existing, call);
            } else {
                mergedCalls.put(id, call);
            }
        }
        
        // 验证完整性并过滤不完整的 tool calls
        return mergedCalls.values().stream()
            .filter(this::isComplete)
            .collect(Collectors.toList());
    }
    
    private void mergeToolCall(ToolCall target, ToolCall source) {
        if ((target.getName() == null || target.getName().isEmpty()) 
            && source.getName() != null && !source.getName().isEmpty()) {
            target.setName(source.getName());
        }
        if ((target.getArguments() == null || target.getArguments().isEmpty()) 
            && source.getArguments() != null && !source.getArguments().isEmpty()) {
            target.setArguments(source.getArguments());
        }
    }
    
    private boolean isComplete(ToolCall call) {
        return call.getId() != null && !call.getId().isEmpty()
            && call.getName() != null && !call.getName().isEmpty()
            && call.getArguments() != null && !call.getArguments().isEmpty();
    }
}
```

#### 2.2 修改 DefaultToolCallingManager

**如果可以直接修改源码，建议在以下位置添加合并逻辑：**

**源码位置：**
- `org.springframework.ai.chat.client.advisor.DefaultToolCallingManager`

**修改建议：**
```java
public class DefaultToolCallingManager implements ToolCallingManager {
    
    @Override
    public List<ToolCall> parseToolCalls(ChatResponse response) {
        List<ToolCall> toolCalls = response.getResult().getOutput().getToolCalls();
        if (toolCalls == null) {
            return Collections.emptyList();
        }
        
        // 添加合并逻辑
        return mergeAndValidateToolCalls(toolCalls);
    }
    
    private List<ToolCall> mergeAndValidateToolCalls(List<ToolCall> rawCalls) {
        Map<String, ToolCall> merged = new LinkedHashMap<>();
        
        for (ToolCall call : rawCalls) {
            String id = call.getId();
            if (id == null || id.isEmpty()) {
                log.warn("Invalid tool call with empty ID, skipping: {}", call);
                continue;
            }
            
            ToolCall existing = merged.get(id);
            if (existing != null) {
                // 合并逻辑
                mergeFields(existing, call);
            } else {
                merged.put(id, call);
            }
        }
        
        // 返回完整的 tool calls
        return merged.values().stream()
            .filter(this::isValid)
            .collect(Collectors.toList());
    }
    
    private void mergeFields(ToolCall target, ToolCall source) {
        // 合并 name
        if (StringUtils.hasText(source.getName()) 
            && !StringUtils.hasText(target.getName())) {
            target.setName(source.getName());
        }
        // 合并 arguments
        if (StringUtils.hasText(source.getArguments()) 
            && !StringUtils.hasText(target.getArguments())) {
            target.setArguments(source.getArguments());
        }
    }
    
    private boolean isValid(ToolCall call) {
        return StringUtils.hasText(call.getId())
            && StringUtils.hasText(call.getName())
            && StringUtils.hasText(call.getArguments());
    }
}
```

### 方案 3：检查流式输出处理逻辑

确保在处理模型的流式输出时，工具调用是完整的，没有被拆分。

**建议：**
- 在流式处理中，等待完整的工具调用块后再进行解析
- 实现缓冲机制，确保工具调用的完整性
- 验证工具调用的完整性（ID、name、arguments 都不为空）

### 方案 4：工具定义和 JSON Schema 验证

确保工具定义和输入参数的描述、必需状态等信息正确无误。

**检查要点：**
- 工具名称不能为空
- 工具参数必须符合 JSON Schema
- 必需参数必须提供
- 参数类型必须正确

**示例：**
```java
@Bean
Function weatherFunction() {
    return Function.builder()
        .name("getWeather")
        .description("Get weather information")
        .inputSchema(JsonSchemaGenerator.builder()
            .title("WeatherRequest")
            .description("Request for weather information")
            .properties(Map.of(
                "location", JsonSchemaProperty.builder()
                    .type("string")
                    .description("Location name")
                    .required(true)
                    .build()
            ))
            .build())
        .build();
}
```

### 方案 5：明确工具调用的格式规范

在调用模型时，明确要求工具调用的格式规范，确保模型输出符合预期。

**在 Prompt 中添加格式要求：**
```
When making tool calls, ensure:
1. Each tool call has a unique ID
2. The 'name' field must not be empty
3. The 'arguments' field must be a valid JSON string
4. Do not split a single tool call into multiple entries
```

## 最佳实践

1. **验证工具调用完整性**：在解析前验证每个工具调用是否包含必需的字段
2. **实现合并逻辑**：对于相同 ID 的工具调用，自动合并 name 和 arguments
3. **错误处理**：对于格式错误的工具调用，记录日志并尝试修复或跳过
4. **测试覆盖**：编写单元测试覆盖各种异常情况
5. **监控和日志**：记录工具调用的解析过程，便于问题排查

## 参考资源

- [Spring AI 官方文档 - 工具调用](https://docs.springframework.org.cn/spring-ai/reference/api/tools.html)
- Spring AI GitHub Issues：搜索相关的问题和解决方案
- Spring AI 社区论坛：获取社区支持

## 更新记录

- 2025-12-26：初始版本，记录工具调用格式错误问题和解决方案

