## Reflection
> What are the key differences between unary, server streaming, and bi-directional streaming RPC (Remote Procedure Call) methods, and in what scenarios would each be most suitable?

Unary is for one request-response. Server streaming is for server sending many request-response in one connection. Bi-directional streaming RPC is for both can sending many request-resposne in one connection.

> What are the potential security considerations involved in implementing a gRPC service in Rust, particularly regarding authentication, authorization, and data encryption?

Authorization is one of security considerations we need to tackle. We need to maintain that the sender has authorization when we use connection for a long time. Not like REST, where we can verify sender authorization in each request.

> What are the potential challenges or issues that may arise when handling bidirectional streaming in Rust gRPC, especially in scenarios like chat applications?

We must make sure there is no race condition. It is because the connection keep sending request-response multineously. It also will effect our server if there are too many bidirectional streaming connection.

> What are the advantages and disadvantages of using the tokio_stream::wrappers::ReceiverStream for streaming responses in Rust gRPC services?

It is asynchronous and easy to integrate with other tokios. But, the tradeoff is the complexity of the code and authorization needed for every request.

> In what ways could the Rust gRPC code be structured to facilitate code reuse and modularity, promoting maintainability and extensibility over time?

gRPC using protobuf for message definitions, or we can say it as interface. It makes to code in rust easier. It can be extended and easier to maintain over time.

> In the MyPaymentService implementation, what additional steps might be necessary to handle more complex payment processing logic?

We can use streaming instead of unary if there are more complex payment processing logic. It will reduce the number of connection need to be created.

> What impact does the adoption of gRPC as a communication protocol have on the overall architecture and design of distributed systems, particularly in terms of interoperability with other technologies and platforms?

It is faster and efficient. We don't need to care much about http method access, because we defined it on our protobuf.

> What are the advantages and disadvantages of using HTTP/2, the underlying protocol for gRPC, compared to HTTP/1.1 or HTTP/1.1 with WebSocket for REST APIs?

HTTP/2 can handle streaming connection and sent it on binary which is more efficient. Hence, gRPC which uses HTTP/2 will have good performance relatively to websocket for REST APIs.

> How does the request-response model of REST APIs contrast with the bidirectional streaming capabilities of gRPC in terms of real-time communication and responsiveness?

REST APIs need new connection for each request-response. In the other hand, gRPC can maintain the same connection for different request-response with the same model.

> What are the implications of the schema-based approach of gRPC, using Protocol Buffers, compared to the more flexible, schema-less nature of JSON in REST API payloads?

gRPC provides protobuf which is an interface for our request-response. It will serialize the incoming data. It will provide what we need. In JSON REST API payloads, it can contain unnecessary data.
