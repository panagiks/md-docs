# Deployment

The RSPET model consists of two modules, RSPET's Server and RSPET's Client module.
The first is located at the attacker/PenTester/Auditor's machine and the later on
the target machine(s).

## Installation

 If you are using a distribution that has a package for RSPET (i.e. BlackArch or ArchStrike) prefer using the distribution's
 package manager to install RSPET.

 If you are in a distribution that doesn't have a package available you can run the following:
 * `pip install --user rspet-server[rest]`
 * `sudo env "PATH=$PATH" rspet-server-setup`

This should take care of all the dependencies.

## Execution

Parameters in `[]` are optional and in `<>` are mandatory.

* `rspet-server [-c #clients, --ip ipToBind, -p portToBind]` - Lunch the server.
* `rspet-server-rest [-c #clients, --ip ipToBind, -p portToBind]` - Lunch the server with RESTful WebAPI (no Console).
* `rspet_client.py <server_ip> [server_port]` - Lunch the client.

## Server Configuration

RSPET's server module in configured through `/etc/rspet/config.json`

Options:
* `"plugins"` - An array of plugin names, if installed will be loaded on server start, if not server will try to install and load them.
* `"log"` - An array (with only one element), sets the lower priority for logging.
* `"plugin_base_url"` - An array of base urls for plugin repos.
* `"certs"` (optional) - A Dictionary with `"crt"` and `"key"` keys provide it to use custom certificates for TLS encryption, if ommited RSPET server will build its own set on its first execution.

## Logging

Logs for RSPET server's execution are stored in `/var/log/rspet/log.txt`.
