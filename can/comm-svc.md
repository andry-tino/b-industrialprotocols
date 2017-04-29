# Communication services

The LLC layer in the CAN protocol defines the function used by upper layers to interact with the bus. It offers basic functinalities which basically are only 2:

- **Send data** Service `L_DATA` is used to broadcast the value for the object being passed. An ID is necessary.
- **Request data** Service `L_REMOTE` is used to ask for the value of a variable whose ID is to be provided.

These primitives are the only available for interacting with the bus.
