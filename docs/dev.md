# Developing Plug-ins

This guide aims to provide help to those developing Plug-ins for RSPET. Before
you start it would be good to use the program a bit (in order to have a level
of familiarity with it's execution flow) and to have a look at RSPET's
[Execution Model](/execution_model) which covers most of the needed background.

## What it is

A Plug-in for RSPET is a python file and more specifically a library (meaning it
is imported).

## Your Checklist

Your plug-in needs to do the following :

* import the plug-in framework
```py
    from Plugins.mount import Plugin
```
* create a class inheriting from `Plugin` e.g.:
```py
    class Essentials(Plugin):
      """
      Class expanding Plugin.
      """
      __server_commands__ = {}
      __cmd_help__ = {}
```

## Going Deeper

Now in order for your plug-in to help a user it has to offer CLI commands. To do
that, in the class created above create an __init__ function. Inside this function
create a new entry to `__server_commands__` Dictionary with your command's name
as an index and an array as a value. Said array should have the function that
executes the code as it's first value and the state's in which the command should
be available in as the rest. Finally, create a new entry to `__cmd_help__`
Dictionary with your command's name as an index and a string containing the
command's syntax. Let's see how this is done with the core command `help`:

```py
    class Essentials(Plugin):
      """
      Class expanding Plugin.
      """
      __server_commands__ = {}
      __cmd_help__ = {}

      def __init__(self):
        """
        Declare plugin's CLI commands their syntax and their scope.
        """
        self.__server_commands__["help"] = [self.help, "basic", "connected", "multiple"]
        self.__cmd_help__["help"] = "help [command]"

      def help(self, server, args): #Note that all functions should take those arguments.
        """List commands available in current state or provide syntax for a command."""
        #Do stuff to print help
        return None #Here you return the desired transition. None takes no "" the rest do.
```

Let's notice a few more things on the previous example. First we see the arguments
passed to help, the first one (ignoring self) is server which an instance of a
[Server Object](#server-object). The second one is args, which is an array of
the arguments the user provided to our command. The number and the validity of
the arguments SHOULD be checked (for missing arguments, type miss-match etc). The
second thing we notice is the functions docstring, when help displays a list of
available commands to the user, it will couple your command with it's docstring
as a description.

## Server Object

In order to communicate with RSPET's server, a plug-in has to interface with an
instance of a Server Object. In order to achieve that the class exposes the following
functions.

| Command        | Description                                                      | Arguments      |
| :------------- | :--------------------------------------------------------------- | :------------- |
| select         | Selects given host(s) based on ids.                              | ids (optional) |
| get_selected   | Interface function. Return selected [hosts](#host-object).       | -              |
| get_hosts      | Interface function. Return all [hosts](#host-object).            | -              |
| execute        | Execute function on all selected client objects.                 | cmd, args      |
| clean          | Remove hosts taged for deletion and unselect all selected hosts. | -              |
| quit           | Interface function. Raise a Quit signal.                         | -              |

## Host Object

Each instance of the Host Object represents a connected client. When a host is
acquired (through either get_hosts or get_selected it too exposes some functions
to help plug-in developers Interface with RSPET.

| Command        | Description                    | Arguments      |
| :------------- | :----------------------------- | :------------- |
| trash          | Gracefully delete host.        | -              |
| purge          | Delete host not so gracefully. | -              |
| send           | Send message to host.          | msg(string)    |
| recv           | Receive from host.             | size (int)     |
