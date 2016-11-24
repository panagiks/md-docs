# Goals Overview

* [Goals](#goals)
* [Todo](#todo)

## Goals

In the short-term goals, it's planned for both server and client to have a
plug-in system implemented.

In the long-term goals, a comprehensive guide has to be created about plug-in
creation so third party plug-ins can easily be created without internal knowledge
of RSPET's design. Along with that a set of rules has to be developed for 3rd
party plug-ins to be officially endorsed, so that information about plug-ins can
be centralized.

In between, bugs and existing design flaws along side feature requests have to be
dealt with.

## Todo

* Fix logic bug where if a direct command's to Host OS execution is perpetual the Server deadlocks
* Add TLS encryption in order to:                                                   =>[DONE]
  * Replace XORing (and subsequently obfuscation with encryption)                   =>[DONE]
  * Verify the "authenticity" of clients
    * A mechanism to issue and verify client certificates
    * A mechanism to recognize compromised client certs
* Add client update mechanism (initial thought was the use of execv but it acts up)
* Add a plugin system to client (a more compact one)
 * Add remote installation of plugins to client
 * Add installed plugins report from client to server
* Add UDP Reflection functionality
* Provide more settings via config file
* Re-introduce multythreading when handling multiple hosts.
* Make commands available with 'Tab' automatically generated based on loaded plugins.
