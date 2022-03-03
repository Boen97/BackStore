## Packet Schdueling

> determining the order in whick queued packets are transmitted over an outgoing link.

- queuing disciplines
1. FIFS (first-come-first-serve)
2. Priority Queuing
3. Round Robin and Weighted Fair Queuing (WFQ)

### Priority Queuing
> packets are classified into priority classes 
> each priority class typically has its own queue
- non-preemptive priority queuing
  > the transimission of a packet is not interrupted once it has begun.
 
### Round Robin and Weighted Fair Queuing

1. Round Robin
- packtes are sorted into classes as with priority queuing
- a round robin scheduler alternates service among the classes 

- work-conserving queuing
  - never allow the link to remain idle whenever there are packets queued for transimission.
  
2. Weighted Fair Queuing 加权公平排队
   - a general form of round robin queuing that has been widely implemented in routers.
   > WFQ differs from round robin in that each class may receive a differential amount of service in any interval of time.
   
