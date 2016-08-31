# CLI Commands

RSPET's server module provides a Command Line Interface (CLI) to its user. This
part aims to introduce RSPET's CLI and detail the available commands.

The commands listed bellow are part of the [`essentials`](#essentials), the
[`files`](#files) and the [`udp`](#udp) plug-ins.

Feel free to ignore the "State(s)" and the "Transition" fields as the will rarely
be of use to an end user and are here purely to assist contributors and Plug-in
developers.

## essentials

|Command       |Description   |Syntax        |State(s)      |Transition    |
|:------------:|:------------:|:------------:|:------------:|:------------:|
| help | List commands available in current state or provide syntax for a command.| `help [command]` | "basic", "connected", "selected" | None |
| Choose_Host | Select a single host. | `Choose_Host <host ID>` | "basic" | "connected" |
| Select | Select multiple hosts. | `Select <host ID [host Id] [host ID] ...>` | "basic" | "multiple" |
| ALL | Select all hosts. | `ALL` | "basic" | "all" |
| Quit | Quit the CLI and terminate the server. | `Quit` | "basic" | None |
| Execute | Execute system command on client. | `Execute <command>` | "connected", "multiple" | None |
| Close_Connection | Kick the selected Client(s). | `Close_Connection` | "connected", "multiple" | "basic" |
| List_Hosts | List all connected hosts. | `List_Hosts` | "basic" | None |
| List_Sel_Hosts | List selected hosts. | `List_Sel_Hosts` | "connected", "multiple" | None |
| Exit | Unselect all hosts. | `Exit` | "connected", "multiple" | "basic" |
| KILL | Stop client(s) from doing the current task. | `KILL` | "connected", "multiple" | None |

## files

|Command       |Description   |Syntax        |State(s)      |Transition    |
|:------------:|:------------:|:------------:|:------------:|:------------:|
| Pull_File | Pull a regular text file from the client. | `Pull_File <remote_file> [local_file]` | "connected" | None |
| Pull_Binary | Pull a binary file from the client. | `Pull_Binary <remote_bin> [local_bin]` | "connected" | None |
| Make_File | Send a regular text file to the host(s). | `Make_File <local_file> [remote_file]` | "connected", "multiple" | None |
| Make_Binary | Send a binary file to the host(s). | `Make_Binary <local_bin> [remote_bin]` | "connected", "multiple" | None |

## udp

|Command       |Description   |Syntax        |State(s)      |Transition    |
|:------------:|:------------:|:------------:|:------------:|:------------:|
| UDP_Flood | Flood target machine with UDP packets. | `UDP_Flood <target_ip> <target_port> [payload]` | "connected", "multiple" | None |
| UDP_Spoof | Flood target machine with UDP packets via spoofed ip & port. | `UDP_Spoof <trgt_ip> <trgt_port> <spoof_ip> <spoof_port> [payload]` | "connected", "multiple" | None |
