# Cloud PubSub

| gcloud pubsub topics create myTopic                          |
| ------------------------------------------------------------ |
| gcloud pubsub topics delete Test1                            |
| gcloud pubsub topics list                                    |
| gcloud pubsub subscriptions create --topic myTopic mySubscription |
| gcloud pubsub topics list-subscriptions myTopic              |
| gcloud pubsub subscriptions pull mySubscription --auto-ack --limit=3 |

### Notes

* Using the pull command without any flags will output only one message, even if you are subscribed to a topic that has more held in it.

* Once an individual message has been outputted from a particular subscription-based pull command, you cannot access that message again with the pull command.
* Fairly MQTT / Kafka behaviors.