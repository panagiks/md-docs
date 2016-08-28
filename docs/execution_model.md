# Server Execution Model

## States

RSPET's CLI is built on a state transition model. In its current version it has
three states, it's either in the "basic" state, the "connected" state or the
"multiple" state. CLI's states directly relate to what the commands provided
affect.

In the "basic" state commands provided affect the server itself.

In the "connected" state commands provided affect the selected client.

In the "multiple" state commands provided affect all the selected clients.

## Transitions

In a state transition model transitions are necessary so that the model can "move"
between states. In RSPET' CLI's model there are five transitions,  "basic" that
will move the model to "basic" state should it be in any other, "connected" that
will move the model to "connected" state only from "basic" state, "multiple" that
will move the model to "multiple" state only from "basic" state, "all" that is
an interface of "multiple" and None that does not affect the model in any way.

The state transition diagram for RSPET's server can be found bellow.

![RSPET's Server state transition diagram](https://github.com/panagiks/RSPET/blob/Beta/Server/CLI_state_diagram.png?raw=true)

# Client Execution Model

TODO
