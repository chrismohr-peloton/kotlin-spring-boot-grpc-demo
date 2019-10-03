# Spring Boot gRPC demo in Kotlin
Example code to show how to make a gRPC server using Spring Boot & gRPC Spring Boot Starter plugin in Kotlin.

## Instructions
Checkout the repo and then do `gradle build` in order to generate the Proto files.

Start the server with `java -jar build/libs/kotlin-grpc-demo-1.0-SNAPSHOT.jar`.

gRPC server will run on port `6565` by default.

## Connect a python client

Install the grpcio-tools package:
```
$ pip install grpcio-tools
```

Use the following command to generate the Python code for the protobuf:
```
$ python -m grpc_tools.protoc -Isrc/main/proto --python_out=. --grpc_python_out=. src/main/proto/demo.proto
```

Run this to connect to the server and make a request:
```
import grpc
import demo_pb2_grpc
import demo_pb2
channel = grpc.insecure_channel('localhost:6565')
stub = demo_pb2_grpc.DemoStub(channel)
request = demo_pb2.DemoRequest()
response = stub.SayHello(request)
print(response)
```
