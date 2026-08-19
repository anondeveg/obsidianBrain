# Problem

a pubsub model is created to fix the following issue:

say we have a a website that sends notifications (publisher)
and we have the user (a reciver)

the website sends the notification and waits for the recivier to verify that it recived it.
the website can't handle other requests while waiting for the recivier to verify. that creates extra unncecary load on the server and makes the whole process way slower than it needs to.

# PUBSUB the solution.

in pubsub (publish subscribe) archetichture we have three main components:
1: publisher
2: message broker
3: recipent
![[Pasted image 20260819181840.png]]

publisher: creates and sends messages **without knowing subscribers**.

subscriber: recives messages from subscribed topics **without knowing publisher**

message broker: routes messages from publisher to subscriber based on thier subscriptions.
it handles errors and problems like that. it also implements on of [[At most once, at least once, exactly once]] requirment levels.

message: the data published

subscription: links between topics and subscribers.

## how it works
subscribers subscribe to topics then when the publisher publishes any message to the topic(channel) the messge broker takes that message and sends it to the subscribers.

result:
The Pub/Sub system allows for asynchronous communication. This means publishers can send messages without waiting for subscribers to be ready, and subscribers can pick up messages whenever it suits them, without needing the publisher to be around.

# Real-World Example

While this resembles Pub/Sub, real systems like Twitter use a hybrid approach involving caching, fan-out strategies, and ranking systems rather than a pure Pub/Sub model.

Publishers: Users post tweets, which are published to the Twitter platform.
    Subscribers: Followers of a user subscribe to their tweets to receive updates.
    Topics: Each user's tweets can be considered a topic, and subscribers receive updates for the topics they are interested in.
    Message Broker: Twitter's backend infrastructure acts as the message broker, routing tweets from publishers to subscribers.
    Message: Each tweet is a message that is published by the user and received by their followers.

In this example, the Pub/Sub architecture allows for scalable and efficient distribution of tweets to followers. Publishers (users) can publish tweets without knowing who will receive them, and subscribers (followers) receive updates in real-time without the need for direct communication with the publishers
Challenges

# The challenges of Pub/Sub Architecture are:

**Message Ordering**: Messages may arrive out of order, causing issues for apps requiring strict sequencing.

**Exactly-once Delivery**: Ensuring no duplicates despite failures is difficult and complex.

**Latency**: Message routing can introduce delays, making low latency hard to balance with scalability and reliability.

**Complexity**: Managing subscriptions, routing, and consistency in large-scale setups requires careful planning.



# Read further
[[what-is-pub-sub]]
https://www.geeksforgeeks.org/system-design/what-is-pub-sub/
Point-to-Point Messaging
