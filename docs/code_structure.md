# Code Structure Overview

## RSPET's Server Module

The server module consists of three classes :

* [API](#API)
* [Console](#console)
* [Server](#server)
* [Host](#host)

## API

The API class acts mostly as an interface class for the [Server](#server) class.
For the time being there are a couple of functions that are completely re-implemented
in the API class but this is to be changed.

Instance Attributes Table

| Attribute Name | Description                          |
| :------------- | :----------------------------------- |
| server         | **Server**. Instance of Server class.|

Class Functions Table

| Function Name  | Description                           |
| :------------- | :------------------------------------ |
| \__init__      | Start server.                         |
| call_plugin    | Call a Plug-in's command.             |
| select         | Interface Server's select function.   |
| help           | Return the entirety of RSPET's help.  |
| refresh        | Interface Server's clean function.    |
| get_server     | Return API's instance of the Server.  |
| get_hosts      | Return hosts.                         |
| quit           | Interface Server's trash function.    |

## Console

The Console class implements the module's Command Line Interface (CLI) and acts
as an interface between the user and the Server class.

Class Attributes Table

| Attribute Name | Description                                                                        |
| :------------- | :--------------------------------------------------------------------------------- |
| prompt         | **String**. The command prompt displayed to the user.                              |
| states         | **Dictionary**. Matching state transition strings to the functions carrying out the transition.|
| state          | **String**. The state module's CLI is currently in.                                |

Instance Attributes Table

| Attribute Name | Description                          |
| :------------- | :----------------------------------- |
| server         | **Server**. Instance of Server class.|


Class Functions Table

| Function Name  | Description                           |
| :------------- | :------------------------------------ |
| \__init__      | Start server and initialize states.   |
| trash          | Delete Console.                       |
| loop           | Main CLI loop. Handles user input.    |
| _basic         | State transition to "basic" state.    |
| _connected     | State transition to "connected" state.|
| _multiple      | State transition to "multiple" state. |
| _all           | Interface of _multiple.               |
| _logo          | Print logo and Authorship/License.    |

## Server

The server class implements the main back-end of the module, managing the server
socket, client selections and Plug-ins.

Instance Attributes Table

| Attribute Name | Description                                                |
| :------------- | :--------------------------------------------------------- |
| connection     | **Dictionary**. See [Connection](#Connection).             |
| commands       | **Dictionary**. Populated by plugins. Is the command switch. |
| clients        | **Dictionary**. See [Clients](#Clients).                   |
| plugins        | **Dictionary**. See [Plugins](#Plugins).                   |
| config         | **Dictionary**. Contains the contets of config.json        |
| quit_signal    | **Boolean**. Used to determine when to quit the Server.    |

### Connection

| Key Name | Description                                                |
| :------- | :--------------------------------------------------------- |
| ip       | **String**. The IP address the server listens on.          |
| port     | **String**. The port the server listens on.                |
| max_conns | **Integer**. The number of connections the server accepts. |
| sock     | **Socket**. The socket that the server listens on.         |

### Clients

| Key Name | Description                                                |
| :------- | :--------------------------------------------------------- |
| hosts    | **Dictionary**. Keys are host IDs. Values are Host instances. |
| selected | **Array**. The IDs of selected hosts.                      |
| serial   | **Integer**. Used to assign serialized IDs to clients.     |

### Plugins

| Key Name | Description                                                |
| :------- | :--------------------------------------------------------- |
| loaded   | **Dictionary**. Keys are plugin names. Values are plugin docstings. |
| installed | **Dictionary**. Keys are plugin names. Values are plugin docstings.|
| available | **Dictionary**. Keys are plugin names. Values are dictionaries. |
| base_url | **Array**. Base urls for plugin repos.                     |

Class Functions Table

| Function Name  | Description                                                                          |
| :------------- | :----------------------------------------------------------------------------------- |
| \__init__      | Initializes attributes, loads Plug-ins and starts listening on socket.               |
| trash          | Safely closes all sockets.                                                           |
| _log           | Log event to file.                                                                   |
| loop           | Main server loop for accepting connections. Execute on separate thread.              |
| setup_command  | Hook function called by plugins to register their commands.                          |
| load_plugin    | Asyncronously load a plugin.                                                         |
| install_plugin | Install a plugin from a loaded repo.                                                 |
| available_plugins | Get a list of all available plugins.                                              |
| installed_plugins | List all plugins installed.                                                       |
| loaded_plugins | Interface function. Return loaded plugins.                                           |
| select         | Selects given host(s) based on ids.                                                  |
| get_selected   | Interface function. Return selected hosts.                                           |
| get_hosts      | Interface function. Return all hosts.                                                |
| execute        | Execute a command on all selected clients.                                           |
| help           | Print all the commands available in the current interface allong with their docsting.|
| clean          | Remove hosts tagged for deletion and unselect all selected hosts.                    |
| quit           | Interface function. Raise a Quit signal.                                             |

## Host

Each Instance of the Host Class represents a connected client.

Class Attributes Table

| Attribute Name | Description                                                                |
| :------------- | :------------------------------------------------------------------------- |
| command_dict   | **Dictionary**. Translates command strings with serialized client commands.|

Instance Attributes Table

| Attribute Name | Description                                               |
| :------------- | :-------------------------------------------------------- |
| deleteme       | **Boolean**. Flag marking Instance for deletion.          |
| sock           | **Socket**. The socket the client is bound to.            |
| ip             | **String**. Client's IP Address.                          |
| port           | **String**. Client's port.                                |
| id             | **Integer**. A serialized ID.                             |
| version        | **String**. Version of the RSPET module running on client.|
| type           | **String**. Type of the RSPET module running on client.   |
| systemtype     | **String**. Client's OS info.                             |
| hostname       | **String**. Client's hostname.                            |

Class Functions Table

| Function Name  | Description    |
| :------------- | :------------- |
| \__init__      | Accept the connection and initialize variables.|
| trash          | Gracefully delete host.                        |
| purge          | Delete host not so gracefully.                 |
| \__eq__        | Check weather two sockets are the same socket. |
| send           | Send message to client.                        |
| recv           | Receive message from client.                   |

## RSPET's Client Module

No content yet. Will update soon.
