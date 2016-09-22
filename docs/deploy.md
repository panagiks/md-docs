# Deployment

The RSPET model consists of two modules, `rspet_server.py` and `rspet_client.py`.
The first is located at the attacker/PenTester/Auditor's machine and the later on
the target machine(s).

## Execution

Parameters in `[]` are optional and in `<>` are mandatory.

* `rspet_server.py [max_connections]` - Lunch the server.
* `rspet_server_api.py` - Lunch the server with RESTful WebAPI (no Console).
* `rspet_client.py <server_ip> [server_port]` - Lunch the client.
