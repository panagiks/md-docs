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
| help | List commands available in current state or provide syntax for a command.| help [command] | "basic", "connected", "selected" | None |
| choose_host | Select a single host. | choose_host <host ID\> | "basic" | "connected" |
| select | Select multiple hosts. | select <host ID [host Id] [host ID] ...\> | "basic" | "multiple" |
| all | Select all hosts. | all | "basic" | "all" |
| quit | Quit the CLI and terminate the server. | quit | "basic" | None |
| execute | Execute system command on client. | execute <command\> | "connected", "multiple" | None |
| close_connection | Kick the selected Client(s). | close_connection | "connected", "multiple" | "basic" |
| list_hosts | List all connected hosts. | list_hosts | "basic" | None |
| list_sel_hosts | List selected hosts. | list_sel_hosts | "connected", "multiple" | None |
| exit | Unselect all hosts. | exit | "connected", "multiple" | "basic" |
| kill | Stop client(s) from doing the current task. | kill | "connected", "multiple" | None |
| create_client_profile | Creates a profile to deploy plugins to clients. | create_client_profile <profile_name> <plugin> [plugin] | "basic", "connected", "multiple" | None |
| list_client_profile | List client profiles. | list_client_profile | "basic", "connected", "multiple" | None |
| apply_client_profile | Deploys a profile to selected clients. | apply_client_profile | "connected", "multiple" | None |

## files

|Command       |Description   |Syntax        |State(s)      |Transition    |
|:------------:|:------------:|:------------:|:------------:|:------------:|
| pull_file | Pull a regular text file from the client. | pull_file <remote_file\> [local_file] | "connected" | None |
| pull_binary | Pull a binary file from the client. | pull_binary <remote_bin\> [local_bin] | "connected" | None |
| make_file | Send a regular text file to the host(s). | make_file <local_file\> [remote_file] | "connected", "multiple" | None |
| make_binary | Send a binary file to the host(s). | make_binary <local_bin\> [remote_bin] | "connected", "multiple" | None |

## udp

|Command       |Description   |Syntax        |State(s)      |Transition    |
|:------------:|:------------:|:------------:|:------------:|:------------:|
| udp_flood | Flood target machine with UDP packets. | udp_flood <target_ip\> <target_port\> [payload] | "connected", "multiple" | None |
| udp_spoof | Flood target machine with UDP packets via spoofed ip & port. | udp_spoof <traget_ip\> <target_port\> <spoofed_ip\> <spoofed_port\> [payload] | "connected", "multiple" | None |
