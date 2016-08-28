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
* Add client update mechanism
* Add UDP Reflection functionality (already in the workings)
* Provide more settings via config file
* Re-introduce multythreading when handling multiple hosts.
* Make commands available with 'Tab' automaticly generated based on loaded plugins.
* Fix logical bug when deleting a client. (Client still shows up on List_Hosts)
* Create comprehensive plug-in creation guide.
