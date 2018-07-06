#[Max-Min Fairness](http://www.mathcs.emory.edu/~cheung/Courses/558/Syllabus/11-Fairness/Fair.html)

A commonly used definition of fairness in computer network is Max-Min fairness.

##Definition

>Maximize the allocation for the most poorly treated flows (with the minimum resource demands), i.e., maximize the minimum.

>Allocation is max-min fair if no rates can be increased without decreasing an already smaller rate.

From Wikipedia:
> In communication networks, multiplexing and the division of scarce resources, max-min fairness is said to be achieved by an allocation if and only if the allocation is feasible and an attempt to increase the allocation of any participant necessarily results in the decrease in the allocation of some other participant with an equal or smaller allocation.

Max-min fairness provides:

1. No flow receives more than its demand,
2. No other allocations satisfying (1) has a higher minimum allocation,
3. Condition (2) recursively holds as we remove the minimal user and reduce the total resource accordingly.

##Advantages and Disadvantages

###Advantages

1. Simple
2. Small players get a big share
3. Everybody gets treated equally

The advantage with max-min fairness over FCFS is that it results in traffic shaping, meaning that an ill-behaved flow, consisting of large data packets or bursts of many packets, will only punish itself and not be able to affect the performance of other (well-behaved) flows. Network congestion is consequently to some extent avoided.

Max-min fair resource sharing results in higher average throughput and better utilization of the resources than a work-conserving **equal sharing** policy of the resources. In equal sharing, some dataflows may not be able to utilize their "fair share" of the resources, because equal sharing would prevent a dataflow from obtaining more resources than any other flow, and from utilizing free resources in the network.

**Fair queuing** is an example of a max-min fair packet scheduling algorithm for statistical multiplexing and best effort packet-switched networks, since it gives scheduling priority to users that have achieved lowest data rate since they became active. In case of equally sized data packets, **round-robin scheduling is max-min fair**.

###Disadvantages

1. Not applicable in complex networks
2. Big players geta small share
3. Easy to manipulate by splitting a flow
4. It is not a continious function

The max-min fairness provides lower average throughput than maximum throughput resource management, where the least expensive flows are assigned all capacity they can use, and no capacity might remain for the most expensive flows. In a wireless network, an expensive user is typically a mobile station at far distance from the base station, exposed to high signal attenuation. However, a maximum throughput policy would result in starvation of expensive flows, and may result in fewer "happy customers".

**A compromise between max-min fairness and maximum throughput scheduling is proportional fairness**, where the resources are divided with the goal to achieve the same cost to each user, or to minimize the maximum cost per unit that a dataflow reaches. Expensive data flows achieves lower service quality than others in proportional fairness, but does not suffer from starvation. Max-min fairness results in more stable service quality, and therefore perhaps "happier customers".

#Proportional Fairness

##Definition

From Wikipedia:
>Proportional fair is a compromise-based scheduling algorithm. It is based upon maintaining a balance between two competing interests: Trying to maximize total wired/wireless network throughput while at the same time allowing all users at least a minimal level of service. This is done by assigning each data flow a data rate or a scheduling priority (depending on the implementation) that is inversely proportional to its anticipated resource consumption.

>Proportionally fair scheduling can be achieved by means of weighted fair queuing (WFQ), by setting the scheduling weights for data flow i to w_{i}=1/c_{i}, where the cost c_{i} is the amount of consumed resources per data bit.

A Network is proportionally fair if and only if:
>Every small change in allocation has a negative effect on the average throughput of each flow in the network.
