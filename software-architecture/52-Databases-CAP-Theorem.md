CAP Theorem states that

**In the presence of a Network Partition, a distributed database cannot guarantee both Consistency and Availability and has to choose only of them**

Network partition - inability to communicate over network due to some network issue. Example, 1 DB replica instance not able to communicate with other ones due to network failure.

1. Forces our database to choose only one **only** where there is a network partition
2. However, majority of time we can easily provide both consistency and availability when there is no network partition & our replicas are able to communicate with each other

## Definitions and Terminology
C - Consistency - every read request receives either the most recent write or an error
A - Availability - every request receives a non-error response, without the guarantee that it contains the most recent write
P - Partition Tolerance - the system continues to operate despite an arbitrary number of messages being lost or delayed by the network between different computers

## Interpretation and Considerations
1. CAP theorem tells us that when we either choose of configure a database we have to drop one of those 3 properties;
- CA - no Partition Tolerance - only with a centralized database, we can avoid network partitions. But with a high amount of data and query volume, it cannot scale.

If we choose to go to distribute route, we have to also choose Partition Tolerance. For that, we have to either drop availability or consistency.
- CP - no availability guarantee
- AP - no consistency guarantee

**We should favor consistency over availability based on use cases. The trade-off should be made during architectural design based on the use case**

