# Remote frame

Remote frames are used by consumers to communicate producers that a certain variable is required. When a node wants a variable to be sent,it will build a remote frame by specifying the variable ID in the _Identifier_ field, it wall set the RTR bit to recessive (`1`) and send the frame broadcast with no data.

The **DLC field** in a remote frame is not set to `0x0` as one might think (given the absence of the _Data_ field). This field is set to the length of the value of the variable being queried, so it has the same value of the DLC field in the corresponding data frame (where RTR is set to `0`).

Remember that since CAN is based on content addressing, consumers do not need to specify an address.