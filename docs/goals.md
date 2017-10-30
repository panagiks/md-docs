# Goals Overview

* [Goals](#goals)
* [Todo](#todo)

## Goals

We are currently accepting feature requests!

In between, bugs and existing design flaws along side feature requests have to be
dealt with.

## Todo

* Add TLS encryption in order to:                                                   =>[DONE]
  * Replace XORing (and subsequently obfuscation with encryption)                   =>[DONE]
  * Verify the "authenticity" of clients
    * A mechanism to issue and verify client certificates
    * A mechanism to recognize compromised client certs
* Add a plugin system to client (a more compact one)                                =>[DONE]
 * Add remote installation of plugins to client
 * Add installed plugins report from client to server
* Add UDP Reflection functionality
* Provide more settings via config file
* Re-introduce multythreading when handling multiple hosts.
