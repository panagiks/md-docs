# Server RESTful WebAPI

This guide aims to cover the usage of RSPET Server module's RESTful WebAPI. The
API consists of GET calls followed by query strings in some cases. It can be
activated by running `rspet_server_api.py` instead of `rspet_server.py`. In order
to use the  RESTful WebAPI you will need to install Flask first. To do that run
`pip2 install Flask flask-cors`. In current version all dependencies are already
installed when running `setup.py`.

## GET Calls

The first Table lists the GET calls that are not followed by a query string and their
functionality.

| URI | Description | Returns |
|:-------------:|:-------------:|:-------------:|
| `/rspet/api/v1.1/refresh` | Refresh server. Check for lost hosts | 204 |
| `/rspet/api/v1.1/hosts`   | Return all hosts | Dictionary. Host ID is key. Unfolds to Dictionary. Keys : `'ip'`, `'port'`, `'version'`, `'type'`, `'hostname'`, `'OS'` |
| `/rspet/api/v1.1/hosts/<string:host_id>` | Return specific host | Dictionary. Keys : `'ip'`, `'port'`, `'type'`, `'uri'`, `'version'`, `'hostname'`, `'OS'` |
| `/rspet/api/v1.1/help` | Return general help | Dictionary. Command is key. Unfolds to Dictionary. Keys : `'help'`, `'states'`, `'syntax'`, `'uri'`|
| `/rspet/api/v1.1/help/<string:command>` | Return command specific help | Dictionary. Keys : `'help'`, `'states'`,  `'syntax'`, `;uri` |
| `/rspet/api/v1.1/quit` | Quit the WebAPI & the Server. | 204 |
| `/rspet/api` | Sitemapish | Array. Unfolds to Dictionary. Keys : `'doc'`, `'methods'`, `'uri'` |


The second Table lists the GET calls when a query string is provided along with their functionality.
These calls replace the POST calls that were used in v1.0. Options in `()` are optional. Returned data
is formated in JSON.

| URI | Description | Query Options | Returns |
|:-------------:|:-------------:|:-------------:|:-------------:|
| `/rspet/api/v1.1/hosts` | Execute command on multiple hosts | `'hosts'`, `'command'`, `('args'(multiple))` | JSON : [Dictionary. Keys : `'transition'`, `'code'`, `'string'`]. HTTP : [200/400/404] |
| `/rspet/api/v1.1/hosts/<string:host_id>` | Execute host specific command | `'command'`, `('args'(multiple))` | JSON : [Dictionary. Keys : `'transition'`, `'code'`, `'string'`]. HTTP : [200/400/404] |
| `/rspet/api/v1.1` | Execute general (non-host specific) command | `'command'`, `('args'(multiple))` | JSON : [Dictionary. Keys : `'transition'`, `'code'`, `'string'`]. HTTP : [200/400/404] |
