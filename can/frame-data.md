# Data frame

Data frames have the RTR field set to dominant (`0`). These frames are used to send values of variables. The ID of the variable is sent in the _Identifier_ field.

## Response Time Analysis
The RTA has been applied to CAN in 1994. 

**Rate Monotonic** The way it was applied was by considering periodic producers in the network and assigning priorities to their messages according to their transmission rates. Data frames for variables being transmitted with lower periods got higher priorities in order to successfully implement a [Rate Monotonic](https://en.wikipedia.org/wiki/Rate-monotonic_scheduling) scheduling. Results were positive.

**Deadline Monotonic** Also in the case of a scheduling following [Deadline Monotonic](https://en.wikipedia.org/wiki/Deadline-monotonic_scheduling), where frames were given higher priorities to lower relative deadlines, the results were positive.

Basically CAN behaves well from a [Response Time](https://en.wikipedia.org/wiki/Response_time_(technology)) point of view.

### 2005-2006
The same RTA was performed again as corrections were made in calculations and simulations. Results were always fine!

## The role of EOF
The EOF field is used to mark the end of a successfully transmitted frame. 

A **transmitting node** considers the frame to be transmitted error-free when no error has been detected until the last bit (7th) of the EOF field.

A **receiving node** considers the frame to be transmitted error-free when no error has been detected until the 6th bit of the EOF field.
