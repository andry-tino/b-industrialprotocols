# Performance Indicators

The different sets of requirements in Industrial Automation caused manufacturers to develop many different protocol stacks efficiently summed up in IEC 61784 in the different PCFs defined in the standard.

CPFs define a structure which is technology based. However IEC 61784-2 facilitates the choice of the proper CP by defining a set of _Performance Indicators_ with the purpose of rating the different CPs under specific perfromance-related quantities.

Every PI has limits and ranges defined in the context of certain conditions, PIs are also connected together by a network of relationships. The use of PIs is supposed to facilitate the detection of the proper CP to be used in a factory or industrial environment which has specific requirements.

## Data capacity PIs
CPs can be categorized basing on transmission capabilites. We find 3 very common PIs targeting this performance measure.

### Delivery time
This PI measures the time needed to convey a [Service Data Unit](https://en.wikipedia.org/wiki/Service_data_unit) (payload of message) from a source node to a destination node. The measurement is performed at Application level, thus the value includes all overheads introduced by the intermediate protocols in the stack.

The standard defines 2 flavors for this PI:

- **Best case scenario** The delivery time is measured in case no transmission error occurs.
- **Lost frame** The delivery time is measured in case one frame is lost, thus retransmission is included in the value.

### Throughput RTE
Throughput $$B_{\text{RT}}$$, expressed in byte/s, of total amount of application data on one single link. If the network defines more links, this PI has to be expressed for each one of them.

### Non-RTE Bandwidth
This is the percentage of bandwidth which can be utilized for non real time traffic. This PI is related to the previous one by the following equation:

$$
B_{\text{NRT}} = B - B \cdot (B_{\text{RT}} + \delta)
$$

So

## Topology 
Relation to delivery time