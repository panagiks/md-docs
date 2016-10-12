# Server RESTful WebAPI

This guide aims to cover the usage of RSPET Server module's RESTful WebAPI. The
API consists of GET and POST calls. It can be activated by running `rspet_server_api.py`
instead of `rspet_server.py`. In order to use the RESTful WebAPI you will need to
install Flask first. To do that run `pip2 install Flask`.

## GET Calls

| URI | Description | Returns |
|:-------------:|:-------------:|:-------------:|
| `/rspet/api/v1.0/refresh` | Refresh server. Check for lost hosts | 204 |
| `/rspet/api/v1.0/hosts`   | Return all hosts | Dictionary. Host ID is key. Unfolds to Dictionary. Keys : `'ip'`, `'port'`, `'version'`, `'type'`, `'hostname'`, `'OS'` |
| `/rspet/api/v1.0/hosts/<string:host_id>` | Return specific host | Dictionary. Keys : `'ip'`, `'port'`, `'type'`, `'uri'`, `'version'`, `'hostname'`, `'OS'` |
| `/rspet/api/v1.0/help` | Return general help | Dictionary. Command is key. Unfolds to Dictionary. Keys : `'help'`, `'states'`, `'syntax'`, `'uri'`|
| `/rspet/api/v1.0/help/<string:command>` | Return command specific help | Dictionary. Keys : `'help'`, `'states'`,  `'syntax'`, `;uri` |
| `/rspet/api/v1.0` | Sitemapish | Array. Unfolds to Dictionary. Keys : `'doc'`, `'methods'`, `'uri'` |

## POST Calls

The content type for all POST calls is application/json and all returns are also
json. Options in `()` are optional.

| URI | Description | Options | Returns |
|:-------------:|:-------------:|:-------------:|:-------------:|
| `/rspet/api/v1.0` | Execute general (non-host specific) command | `'command[str]'`, `('args[array[str]]')` | JSON : [Dictionary. Keys : `'transition'`, `'code'`, `'string'`]. HTTP : [200/404] |
| `/rspet/api/v1.0/hosts/<string:host_id>` | Execute host specific command | `'command[str]'`, `('args[array[str]]')` | JSON : [Dictionary. Keys : `'transition'`, `'code'`, `'string'`]. HTTP : [200/400/404] |
| `/rspet/api/v1.0/hosts` | Execute command on multiple hosts | `'command[str]'`, `'hosts[array[int]]'`, `('args[array[str]]')` | JSON : [Dictionary. Keys : `'transition'`, `'code'`, `'string'`]. HTTP : [200/400/404] |
