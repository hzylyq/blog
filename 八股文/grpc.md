gRPC 支持四种通信模式，分别适用于不同的应用场景。这些模式基于 HTTP/2 协议，充分利用了其双向流和多路复用等特性。以下是 gRPC 的四种主要模式：

---

### 1. **Unary RPC（一元 RPC）**
   - **描述**：最简单的 RPC 模式，客户端发送一个请求，服务器返回一个响应。
   - **适用场景**：传统的请求-响应模型，类似于 REST API。
   - **示例**：
     ```proto
     rpc SayHello (HelloRequest) returns (HelloResponse);
     ```
     - 客户端调用 `SayHello`，发送一个 `HelloRequest`，服务器返回一个 `HelloResponse`。

---

### 2. **Server Streaming RPC（服务器流式 RPC）**
   - **描述**：客户端发送一个请求，服务器返回一个流式的响应（多个消息）。
   - **适用场景**：服务器需要向客户端发送大量数据或实时数据（如日志推送、实时监控）。
   - **示例**：
     ```proto
     rpc LotsOfReplies (HelloRequest) returns (stream HelloResponse);
     ```
     - 客户端调用 `LotsOfReplies`，发送一个 `HelloRequest`，服务器通过流式响应返回多个 `HelloResponse`。

---

### 3. **Client Streaming RPC（客户端流式 RPC）**
   - **描述**：客户端发送一个流式的请求（多个消息），服务器返回一个响应。
   - **适用场景**：客户端需要上传大量数据或分批次发送数据（如文件上传、批量处理）。
   - **示例**：
     ```proto
     rpc LotsOfGreetings (stream HelloRequest) returns (HelloResponse);
     ```
     - 客户端通过流式请求发送多个 `HelloRequest`，服务器返回一个 `HelloResponse`。

---

### 4. **Bidirectional Streaming RPC（双向流式 RPC）**
   - **描述**：客户端和服务器可以同时发送和接收多个消息，形成一个全双工的通信流。
   - **适用场景**：实时交互场景（如聊天应用、实时游戏、协作编辑）。
   - **示例**：
     ```proto
     rpc BidiHello (stream HelloRequest) returns (stream HelloResponse);
     ```
     - 客户端和服务器通过流式请求和响应进行双向通信。

---

### 模式对比

| 模式                     | 客户端请求       | 服务器响应       | 适用场景                           |
|--------------------------|------------------|------------------|------------------------------------|
| **Unary RPC**            | 单个请求         | 单个响应         | 简单请求-响应（如 REST API）       |
| **Server Streaming RPC** | 单个请求         | 流式响应         | 服务器推送数据（如日志、监控）     |
| **Client Streaming RPC** | 流式请求         | 单个响应         | 客户端上传数据（如文件上传）       |
| **Bidirectional RPC**    | 流式请求         | 流式响应         | 实时交互（如聊天、游戏）           |

---

### 示例代码

#### Unary RPC
```proto
service Greeter {
  rpc SayHello (HelloRequest) returns (HelloResponse);
}
```

#### Server Streaming RPC
```proto
service Greeter {
  rpc LotsOfReplies (HelloRequest) returns (stream HelloResponse);
}
```

#### Client Streaming RPC
```proto
service Greeter {
  rpc LotsOfGreetings (stream HelloRequest) returns (HelloResponse);
}
```

#### Bidirectional Streaming RPC
```proto
service Greeter {
  rpc BidiHello (stream HelloRequest) returns (stream HelloResponse);
}
```

---

### 选择模式的建议
1. **简单请求-响应**：使用 **Unary RPC**。
2. **服务器推送数据**：使用 **Server Streaming RPC**。
3. **客户端上传数据**：使用 **Client Streaming RPC**。
4. **实时双向通信**：使用 **Bidirectional Streaming RPC**。

---

gRPC 的四种模式提供了灵活的通信方式，能够满足不同场景的需求。根据具体的业务逻辑和数据交互方式，选择合适的模式可以显著提高系统的性能和开发效率。