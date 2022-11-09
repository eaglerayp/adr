# WebSocket Solution Discussion / ADR

## Status

Implement/POC self-build websocket server and using pubsub service. (first trial using AWS IoT Core as pubsub)

## Background/Context

We need a solution to push event/message to frontend to replace current API polling mechanism.

First plan was directly using MQTT over Websocket of AWS IoT Core by web directly, but after some trial and discussions, we found there is a risk we cannot protect AWS IoT Core DDoS from exposed websocket entry. 

- AWS IoT doesn’t provide user based (Cognito unauth) policy.
- AWS IoT lack of mechanism to ban one Cognito/websocket client.

Thus, attacks could DDoS the IoT Core by burst connecting websocket.  (There is AWS limit on connecting per account)

## Date

2022 Oct~ 2022 Nov. 9th

## Decision

Not expose AWS IoT Core to frontend, backend provide websocket functionality of frontend, then backend could do further protection and switch pub-sub solutions with more flexibility