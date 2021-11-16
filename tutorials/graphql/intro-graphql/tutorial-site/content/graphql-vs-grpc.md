---
title: "GraphQL vs gRPC"
metaTitle: "GraphQL vs gRPC | GraphQL Tutorial"
metaDescription: "GraphQL vs gRPC. A comparison of GraphQL and gRPC APIs, highlighting the key differences with examples and in detail about how they complement each other "
---

gRPC is an open source remote procedure call system developed by Google as a follow up to Stubby. Similar to GraphQL, it is a specification and hence language independent.

![gRPC](https://lh3.googleusercontent.com/po_JLnNNjHUaJqBlVf6BRqFWj2jzxCuCcGaLol4ho38UnhnKprQipoHJkRnvDdznnCxQxbr050yUEkFuikhbk_NxvtSwUN1W2V3VsA-I_Bfa71WrpSRkSkidnJpgDUbgXG2t-deT=s1600)

## gRPC Data Format

The data format used in gRPC is one of the fundamental differences in comparison to GraphQL/REST APIs. gRPC uses Protocol buffers binary format for data exchange. The typical data format with GraphQL or REST API is simple text based data. Naively put, gRPC uses lesser size for data transport and hence the request response can be relatively faster.

For example, in a simple GraphQL request, we use the JSON request / response body and send it over HTTP. But with gRPC, the request body is in binary format called the protocol buffers, although JSON can also be used.

## proto file

Both the client and server needs to have the same schema definition, written in a `.proto` file. This file contains the definitions by which data is encoded and decoded to and from the Protocol Buffers binary format.

In GraphQL, you typically define the schema and types on the server. The client does not need to redefine them again. Introspection of the server can give access to the schema on the client.

Here's a simple example:

```
message Person {
  string name = 1;
  int32 id = 2;
  bool has_ponycopter = 3;
}
```

With the definitions, you can use the `protoc` compiler to generate data access classes in preferred language of choice. gRPC runtimes are available in all popular languages including C++, Go, Node, Java, Python, Ruby etc.

```
// The greeter service definition.
service Greeter {
  // Sends a greeting
  rpc SayHello (HelloRequest) returns (HelloReply) {}
}

// The request message containing the user's name.
message HelloRequest {
  string name = 1;
}

// The response message containing the greetings
message HelloReply {
  string message = 1;
}
```

## HTTP/2 support

gRPC is designed for HTTP/2 protocol and hence supports the bi-directional data exchange, useful for asynchronous use cases. For example, due to the support for HTTP/2, a client or a server can open a connection and unless either of them close it, it can stay live and serve any number of requests.

It can allow any number of requests or data streams too, bidirectionally. Returning in data streams lets you build real time apps similar to GraphQL.

In GraphQL, real time apps are built using websocket protocol as most server implementations make use of that.
