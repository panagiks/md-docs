# Server API

This guide aims to help you utilize RSPET Server's API to create programs that
interface with it. It will focus on the higher level API (as you can also manually
create and interface each class on a lower level). Because this API was created
with the upcoming RESTful WebAPI in mind it is stateless. This means that the
developer will have to deal with the states, although state transitions that would
normally take place are exposed through the API.

## Using RSPET Server's API

In order to access RSPET Server's API you have to include `rspet_server.py`.
Following this you have to create an instance of the rspet_server.API Class. This
will in turn create an instance of the Server class. The previous steps will have
a result equal to lunching RSPET's Server directly from a command line.

## API's Functions

| Function     | Description  | Arguments    | Returns      |
|:------------:|:------------:|:------------:|:------------:|
| __init__     | Called during instance creation | - | Raises socket.error if there is an error during binding|
| call_plugin  | Call a command defined in a plug-in | command(string), args(array) | Dictionary. Keys : `'transition'`, `'code'`, `'sting'` |
| select       | Manage host selection | hosts(array) | Dictionary, contains transition, code and sting |
| help         | Return all available Commands, their syntax and their documentation | - | Dictionary. Command is Key. Unfolds to Dictionary. Keys : `'help'`, `'syntax'`, `'states'` |
| refresh      | Interfaces Server's clean function. Checks for lost hosts. | - | - |
| get_server   | Return the API's instance of Serve. Used for lower level interaction. | - | Instance of Server class |
| get_hosts    | Return all available hosts | - | Dictionary. Host ID is key. Unfolds to Dictionary. Keys : `'ip'`, `'port'`, `'version'`, `'type'`|

## RSPET Server's ReturnCodes

RSPET's Server module has a class containing the Return codes that command execution
can result in. They are accessible under rspet_server.ReturnCodes.<CodeName>. The
Return Codes currently available are the following.

| Code Name     | Value (Int)   |
|:-------------:|:-------------:|
| OK                | 0             |
| InvalidSyntax     | 1             |
| SocketError       | 2             |
| LocalAccessError  | 3             |
| RemoteAccessError | 4             |
| OutOfScope        | 5             |
| CommandNotFound   | 6             |
| InvalidHostID     | 7             |

## Sample code

Now, let's have a look at some sample code. Create a new python project in the same
directory as `rspet_server.py` (let's call it `api_test.py`).

```py
    import rspet_server

    rspet_api = rspet_server.API()
    output = rspet_api.call_plugin("help")
    state_transition = output['transition']
    return_code = output['code']
    return_string = output['string']
    if return_code != rspet_server.ReturnCodes.OK:
      print ("Ooops. I've got an error. It says :\n%s" %return_string)
    else:
      print return_string
```

Executing the above code will give us the following output.

```
    Server commands:
    Quit: Quit the CLI and terminate the server.
    ALL: Select all hosts.
    help: List commands available in current state or provide syntax for a command.
    Choose_Host: Select a single host.
    List_Hosts: List all connected hosts.
    Select: Select multiple hosts.
```
