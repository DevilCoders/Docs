Execute ```make build``` to regenerate source code for grpc gateway.
Do not try to implement it using ya.make, it wont work:
1. grpc-gateway is severely outdated, and grpc-gateway/v2 - relatively not outdated - is not integrated into ya.make
2. RUN_PROGRAM attempts to check .proto for correctness and fails because it can't understand includes.
