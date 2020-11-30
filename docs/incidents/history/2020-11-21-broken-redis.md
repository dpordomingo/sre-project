# Disconnected Redis

## TL;DR

|  |  |
| --- | --- |
| started | `2020-11-21 12:50 CET` |
| detected | `2020-11-21 13:00 CET` |
| restored | `2000-31-12 13:30 CET` |
| closed | `2000-31-12 13:40 CET` |
| | |

The counter service stopped working for 40 minutes because the database provider decided to run a simulacrum without noticing its users.

There was no data loss because, at that time, there were no counter users. The severity of the issue was HIGH because if there had been users by that time, many would have lost their positions.

It's decided to look for a more reliable database provider, and in the meanwhile, to run our solution. Given it's only needed some investigation about other providers, the transition can take only a couple of days.


## Description of the Incident

While working on the counter's scalability, the development team realized that the system was failing and not returning any position at all, no matter the `:id` it would be used. The issue was caused because the Redis server was down.

The Redis provider, which stores the position, confirmed that they were doing a simulacrum when they decided to stop the service. Once they got some complaints from other customers, they decided to restore the service. The provider was not able to confirm how much data was lost.

Once the Redis server was restarted, the service returned to normality.

Since there were no users at that time, there was no data loss.


## Consequences. Negative Impact

When Redis is not configured to persist the data, it relies on default implementations, depending on each provider installation. It was not clear on this situation, but they said it could be persisted every 5 minutes (300 seconds).

A real scenario with 100k/second would mean that it could be lost 30 million positions.

In this case, no position was lost because, at that moment, the service was not attending users.


## Risk Analysis

The team didn't consider that the provider would stop the service on purpose without formal notification. It's something strange in the market, but once it happens, our current service is not prepared to act correctly, and errors till Redis is restarted.

The chances of this to happen are relatively high given the provider does not transmit any confidence nor offer any reliable way to communicate these interruptions of service beforehand.


## Action Plan

Since the Redis provider is not reliable, we decide to:
- spin up our own Redis instance, and configure it to persist every second,
- look for another provider offering at least 99.999% of availability,
- set up an alert when the service is returning more than 1 errors per second or 2k errors per month,
- set up an alert when 5% requests during a second take more than 100ms,
- make sure the counter is returning a `503 Service Unavailable` error when a known downtime event causes it; the body of the response should link to more details,
- make sure the system can self recover from Redis outages, and implement e2e tests covering such situations,
- develop a [framework to deal with incidents](../README.md), and a normalized way to develop postmortems,
- make sure the dev and ops team are aware of this incident.


## Addendum. Timeline

_Timeline with signals, alerts, failures, consequences, and actions__

All events below happened on `2020-11-21`, hours in `CET`

`12:50` The external service offering Redis was stopped by its owner to evaluate what would happen.

`13:00` The team in charge of the development of the counter service realizes that the HTTP requests they're manually doing are failing.

`13:01` The team runs some performance tests to see if the counter is down or it's a service degradation. It is run some performance test from another instance in the same network in a period of 4 mins, and all of them fail, so it's discarded a temporal issue.

`13:05` It's manually run the counter service from a local development machine and tested against it, and it's confirmed that Redis is not answering.

`13:08` Since Redis is not managed by the team, it's decided to complain to the provider.

`13:15` The Redis provider confirms the issue and explains the server was stopped to see what would happen in a sort of simulacrum. They agree to communicate this kind of operation in advance.

`13:30` Redis service is restarted, and the counter service works again.

`13:40` The team confirms no customers were accessing the counter when the service was down, so they didn't lose their existent positions.


## Addendum: Interview Minutes

Communication from the Redis provider `2020-11-21 13:15 CET`.

```
We decided to do a simulacrum of a Redis fault by stoping the service some
minutes ago.

The simulacrum went well since we started receiving complaints from some users.

We agree on this should be avoided in the future, so we'll let you know in
advance with a message in the Slack channel.
```

Once asked about the persistence of the cache, the Redis provider said:

```
We didn't configure any persistence by hand, so we guess it will be using its
default settings for persisting cache to disc.

We guess we could set the persistence to 1s.
```
