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

## API & RESTful WebAPI

Since the API was initially designed to serve the RESTful WebAPI and since the
later is by definition stateless, both the API and WebAPI are stateless. This does
not mean that the states are not available or that the state model changes, it means
that the states are not "active" when using either API. Despite that, state transitions
that would normally occur are exposed through both APIs (they are returned one way
or another). So it is up to the developer utilize either API to implement and manage
the states.

# Client Execution Model

TODO
