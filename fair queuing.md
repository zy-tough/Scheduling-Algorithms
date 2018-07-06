# [Generalized Processor Sharing](http://www.mathcs.emory.edu/~cheung/Courses/558/Syllabus/11-Fairness/GPS.html)



From Wikipedia: 
>GPS is "an idealized scheduling algorithm that achieves
perfect fairness. All practical schedulers approximate GPS and use it as a
reference to measure fairness."

>   Generalized processor sharing assumes that traffic is fluid (infinitesimal
>   packet sizes), and can be arbitrarily split. There are several service
>   disciplines which track the performance of GPS quite closely such as
>   weighted fair queuing (WFQ), also known as packet-by-packet generalized
>   processor sharing (PGPS).

 

Such a server is known in queuing theory as an **Exponential Server**.

-   The exponential server can "split" itself into an arbitrary number of
    "smaller" (less capable) servers.

-   Each of these "smaller" servers can work on a different job.

-   All jobs in the queue of the exponential server are worked on
    simultaneously.

The General Processor Sharing technique can be generalized by assigning weights
(representing "importance" or "priority") to the different jobs.

 

# [Fluid Flow Server](http://www.mathcs.emory.edu/~cheung/Courses/558/Syllabus/11-Fairness/GPS.html)

 

The Fluid Flow Server (FFS) is the network equivalent of the Exponential Server
and is to establish the BEST fairness of sharing. It can give us an idea how
good a solution is compared to the ideal solution.

The FFS is only an idealized transmission method (representing the general
processor sharing technique). However, a router must transmit a packet
atomically (unsplit) because the structure of the packet must remain intact. The
FFS server does not send packets atomically (it mixes bits from different
packets), and hence the FFS server cannot be used to forward packets.

 

# [Weighted Fair Queueing](http://www.mathcs.emory.edu/~cheung/Courses/558/Syllabus/11-Fairness/WFQ.html)


From Wikipedia:
>Fair queuing is a family of scheduling algorithms used in some
process and network schedulers. The algorithm is designed to achieve fairness
when a limited resource is shared, for example to avoid flows with large packets
or processes that generate small jobs to consume more throughput or CPU time
than other flows or processes.

>   Weighted fair queueing (WFQ) is a network scheduler scheduling algorithm. WFQ is both a packet-based implementation of the generalized processor sharing (GPS) policy, and a natural extension of fair queuing (FQ). Whereas FQ shares the link's capacity in equal subparts, WFQ allows schedulers to specify, for each flow, which fraction of the capacity will be given.

WFQ is a packetized approximation for FFS/GPS. Its major contribution is a
virtual time method to compute the termination time of a packet transmission
easily.

-   WFQ transmits a packet in its entirety before transmitting the next packet.

-   **WFQ selects the packet with the smallest finish time under the FFS
    transmission method.**

-   **Virtual time is used to simulate the FFS transmission.** The virtual clock
    keeps tracks of the progress of the packet transmissions in the FFS server.
    When a packet arrives, the virtual finish time of that packet can be
    computed immediately using the virtual time system.


# Deficit Round Robin


From Wikipedia: 
>Deficit Round Robin (DRR), also Deficit Weighted Round Robin
(DWRR), is a scheduling algorithm for the network scheduler. **DRR is, like
weighted fair queuing (WFQ), a packet-based implementation of the ideal
Generalized Processor Sharing (GPS) policy.** It was proposed by M. Shreedhar
and G. Varghese in 1995 as an efficient (with O(1) complexity) and fair
algorithm.


# Token Bucket and Leaky Bucket


Token Bucket and Leaky Bucket are traffic shaping methods.


From Wikipedia:
>The token bucket is an algorithm used in packet switched computer networks and telecommunications networks. It can be used to check that data transmissions, in the form of packets, conform to defined limits on bandwidth and burstiness (a measure of the unevenness or variations in the traffic flow). It can also be used as a scheduling algorithm to determine the timing of transmissions that will comply with the limits set for the bandwidth and burstiness: see network scheduler.

>The leaky bucket is an algorithm based on an analogy of how a bucket with a leak will overflow if either the average rate at which water is poured in exceeds the rate at which the bucket leaks or if more water than the capacity of the bucket is poured in all at once, and how the water leaks from the bucket at an (almost) constant rate. It can be used to determine whether some sequence of discrete events conforms to defined limits on their average and peak rates or frequencies, or to directly limit the actions associated to these events to these rates, and may be used to limit these actions to an average rate alone, i.e. remove any variation from the average.


**Leaky bucket:**

Parameters: rate
1. Smooth out traffic by transmitting packets at a constant rate.
2. Does not permit burstiness (Bursty traffic is converted into uniform traffic).
3. If bucket is full, packets are discard.
4. Application: Traffic shaping or traffic policing.

**Token bucket:**

Parameters: rate, burstiness.
1. The bucket holds tokens generated at regular intervals of time and has has maximum capacity. If there are tokens in the bucket and a ready packet, a token is removed from the bucket and the packet is send.
2. Token bucket smooths traffic too but permits burstiness - which is equivalent to the number of tokens accumulated in the bucket. It allows the output rate vary depending on the size of burst.
3. Discard tokens (never discard packets) when bucket is full.
4. Application: Network traffic shaping or rate limiting.


Token-bucket filters provide an alternative to fair queuing for providing a traffic allocation to each of several groups. The main practical difference between fair queuing and token bucket is that if one sender is idle, fair queuing distributes that sender’s bandwidth among the other senders. Token bucket does not: the bandwidth a sender is allocated is a bandwidth cap.

Combining fair queuing with token bucket might seem improbable: the goal of fair queuing is to be work-conserving, allowing the bandwidth assigned to an idle input class to be divided among the active input classes, and the goal of token bucket is generally to limit a class to its token-bucket-defined maximum transmission rate. The usual approach to a hierarchy-based synthesis is to allow the administrator to decide, at each node of the hierarchy, whether or not the node can “borrow” (without repayment) bandwidth from inactive siblings. If it can, the set of siblings with mutual borrowing privileges resembles a fair-queuing scheduler; if not, the node is more like a token-bucket scheduler.


# Reference

[An Introduction to Computer Networks - Queuing and Scheduling](<https://intronetworks.cs.luc.edu/current/html/queuing.html>)

[Scheduling and Policing Mechanisms](<http://www2.ic.uff.br/~michael/kr1999/6-multimedia/6_06-scheduling_and_policing.htm>)

[What is the difference between token bucket and leaky bucket algorithms?](https://www.quora.com/What-is-the-difference-between-token-bucket-and-leaky-bucket-algorithms)

[General Processor Sharing, Weighted Fair Queueing, and Deficit Round Robin](<http://www.mathcs.emory.edu/~cheung/Courses/558/Syllabus/11-Fairness/>)

