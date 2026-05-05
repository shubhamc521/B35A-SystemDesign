
There are multiple microservices.

1.
Service A is sending msg to Service B but Service is not aviable.
If not avialble, I will retry for a while and I will stop. Message will get lost.

2.
Service B: -------- Depositing the Money
Service A: -------- Withdraw(UPI)

Service B is comming first and then Service A but somehow Service A req is handled first.
--> Insuffient Balance

Order should be maintained.

[ Queue - All the msg, will be stored in this queue and processed in sequencial manner]

[YT Channel 1]
Publisher A: --------                            ----Subscriber X. - YT Channel 1
                    -------[EventBus YT1, YT2]----   Subscriber Y. - YT Channel 2
Publisher B: --------                            ----Subscriber Z. - YT Channel 1,2
[YT Channel 2]

Event Bus can PUSH the message to the interested Subscriber.
OR
Subscribers can PULL the message from the event bus.

Publishers == Producers
Subscriber == Consumers


Key Concepts:
Events = Events are messages or notif about a change or action that has happened. [New Video Uploaded (Update/Action)]
                                                                                  [User Updates / Linkedin Post]

Publisher-Subscriber Model:
                    - Publisher: These are event producers. [ YT Channel 1]
                    - Subscribers: They listen for specific events. [Subscriber 1 is listening to YT channel 1's updates]

Benifits of Event Bus:
                    - Loose Coupling: Publisher and Subscribers are independent. Its easier to maintain and scale.
                    - Asynchrouns Communication: Publisher can publish the msg and subscriber can process the msg according to there own pace.
                    - Event Driven: PaymentProccesed ----> OrderPlaced --------> OrderShipped.
                                    What happens if I ship the order before payment? Is it the right right?
                                    Event should happen proper order only.

Partition Events by Topic:
                
                Bosscoder Academy:       Arrays                       #DSA #Code             Person1 interested in DSA thing.
                Coders Academy:          Linkedlist, SystemDesign     #DSA #Linkedlist       Person2 interested in DSA and HLD both
                                                      #HLD


                Event Bus:

                        DSA : -----------------Array, LinkedList------                      Person1 interested in DSA thing
                        HLD : -----------------SystemDesign-----------                      Person2 was interested in system design
                        Code: -----------------Array, LinkedList------

                        These DSA Bus and HLD Bus are called as Topics.

                        One Subscriber can subscribe to multiple topics.
                        One Publisher can publish to multiple topics.

                        Single Topic: Event will be be pusblished to queue matching the event type.
                        Multiple Topic: Some events will be associated with multiple topics, they will be published to all the topics.


Idempotency:
 - Ensures event is proccessed only once. Even if it is published multiple times.

 Deposit money in bank, -- Multiple requests are published by the deposit microservice in the queue.
                           It will get published multiple times.
                           THat's wrong?

                           Mechanism:
                           - UniqueEventID
                           - Deduplication logic: subscriber should be able to check if the event is already proccesssed or not.

                           If order event is published twice, the payment service should only charge the customer once.

Handling Failures and Retrying events:

- Failure Handing: If event bus fails to get ACK from subscriber, the event bus should RETRY.
- Retries:
        Exponential backoff: Retry after incresingly longer interval. [ You enter wrong password, your phone waits for 10sec, next wrong attempt try it after 20sec and it goes on]

        Max Retry Limit: A limit on Retry.

PUSH/PULL Mechanishm:

    PUSH: Event bus should be able to PUSH the event to the subscribers.
    PULL : Subscriber should be able to PULL evetns from the event BUS.

    PULL after ID/Time:
    Subscriber can request all the events from that ID/timestamp.

---------------------------------------------------

Ordered Event Proccesing:
    Sequencial Delivery: Event Should be delivered in the order they are published. One at a time. [Logical Clocks like Vector clocks]


    Transactional Proccessing: if event A fails, Event b should not be proccessed.

    EX: PaymentProcess fails then orderplaced event should not happen.
        OrderShip event should not heppen before orderplaced event is proccessed succesfully.

Bus Mechanics:

    Casual Ordering:
        If event A happens before B, then event A should be proccsed before B.

        Threads for casual ordering:
        We will signal all the related events to the same thread.

    Coarse Grained Ordering:
        Topic Level Ordering: All the events in that specific topic should be proccesed in the order they are received.
        Hashing for TOpic Level Ordering: h(TopicID) % size. This will ensure that the event from the same topic goes to same thread.

        Ordering Publishers:
        Multiple publishers can send the event to the same topic. All the events belonging the topic need to ordered currectly.

        Thread will be assigined to publishers based on topic hash.

Dead Letter Queue:
    If Event cannot be successfully proccessed by the subscriber after RETRY, The event will be pushed to DLQ.

    Use:
    Send the failedEvents again.
    Capture the failure logs.
    Prevent the blocking of event proccessing.


Design A EventBus:

- Requirement & Architecture
- Data Models
- Core EventBus
- Keyed Executor - (Thread Mechanism)
- Retry Mechanism
- Dead Letter Queue
- Testing 
- Trade-Off

1. Requirements:

Functional:
- Publish Events to Topics
- Subcribe (PUSH/PULL)
- Retry with BackOFF
- Dead Letter Queue.
- Event Replay
- Direct Lookup

Non Functional:
- Thread Safe
- Ordered with topics
- O(1) Operations
- At least one delivery


Architecture:


PUBLISHER ---[Pubish]------EventBUS-------[Route]-------Topics-------[PUSH]------PushSub ---- RETRY --[MAX]---DLQ
                                                                     [PULL]------PullSub



















                   
















