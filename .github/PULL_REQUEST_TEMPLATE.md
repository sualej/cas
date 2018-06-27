<!--

# Contributing

First off, thank you for considering to contribute to CAS. 

# Details

Closes #IssueNumber

Ensure that you include the following:

- [] Brief description of changes applied
- [] Any documentation on how to configure, test
- [] Any possible limitations, side effects, etc
- [] Reference any other pull requests that might be related.

-->

Actually we are using version 5.2.3 and we have found problems with concurrent users when we try to get a proxy ticket.

java.util.ConcurrentModificationException: null
        at java.util.HashMap$ValueSpliterator.tryAdvance(Unknown Source) ~[?:1.8.0_172]
        at java.util.stream.ReferencePipeline.forEachWithCancel(Unknown Source) ~[?:1.8.0_172]
        at java.util.stream.AbstractPipeline.copyIntoWithCancel(Unknown Source) ~[?:1.8.0_172]
        at java.util.stream.AbstractPipeline.copyInto(Unknown Source) ~[?:1.8.0_172]
        at java.util.stream.AbstractPipeline.wrapAndCopyInto(Unknown Source) ~[?:1.8.0_172]
        at java.util.stream.FindOps$FindOp.evaluateSequential(Unknown Source) ~[?:1.8.0_172]
        at java.util.stream.AbstractPipeline.evaluate(Unknown Source) ~[?:1.8.0_172]
        at java.util.stream.ReferencePipeline.findFirst(Unknown Source) ~[?:1.8.0_172]
        at org.apereo.cas.ticket.TicketGrantingTicketImpl.trackServiceSession(TicketGrantingTicketImpl.java:189) ~[cas-server-core-tickets-5.2.3.jar:5.2.3]
        at org.apereo.cas.ticket.ProxyGrantingTicketImpl.grantProxyTicket(ProxyGrantingTicketImpl.java:83) ~[cas-server-core-tickets-5.2.3.jar:5.2.3]
        at org.apereo.cas.ticket.factory.DefaultProxyTicketFactory.produceTicket(DefaultProxyTicketFactory.java:70) ~[cas-server-core-tickets-5.2.3.jar:5.2.3]
        at org.apereo.cas.ticket.factory.DefaultProxyTicketFactory.create(DefaultProxyTicketFactory.java:57) ~[cas-server-core-tickets-5.2.3.jar:5.2.3]
....


Syncronized directive it is only applied into validateServiceTicket. is not needed to syncronized all the methods? Like grantProxyTicket method where we get the exception? 
We have found comments in the code like "Is this synchronization needed here?" in validateServiceTicket... 

I think is needed in all of them. 
 
