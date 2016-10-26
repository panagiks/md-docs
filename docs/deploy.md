# Deployment

The RSPET model consists of two modules, `rspet_server.py` and `rspet_client.py`.
The first is located at the attacker/PenTester/Auditor's machine and the later on
the target machine(s).

## Execution

Parameters in `[]` are optional and in `<>` are mandatory.

* `rspet_server.py [max_connections]` - Lunch the server.
* `rspet_server_api.py` - Lunch the server with RESTful WebAPI (no Console).
* `rspet_client.py <server_ip> [server_port]` - Lunch the client.

## Development Deployment

Additionally, RSPET provides a Deployment Tool to assist in Development and Testing.
In order to setup the Testing environment and lunch the preferred version along
with a few instances of the client run the following from RSPET's root folder:

* `run_dev.py -c <num_of_clients_to_spawn> [--rest]`

In order for the built-in cleanup methods to work correctly, either version of
the server has to be terminated correctly (Either provide `Quit` to the CLI or
make a GET request at /rspet/api/v1.0/quit).
If for any reason the cleanup methods were omitted (The server was forcefully
terminated or the Development Deployment script crashed), manually remove the
`test/` directory. 
