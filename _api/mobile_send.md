---
title: /mobile/send
position: 27
type: post
description: Send a push notification to the provided objects
---
users_id
: The ids of the objects previously stored to send push notification

payload
: The payload of the push notification

expiry
: The expiry of the push notification, only for iOS

identifier
: The identifier for the push notification, only for iOS

Send a push notification to the provided objects in the token platform registered
{: .success }

~~~ shell
curl -i -XPOST -H "Ckey: YOUR_APP_CKEY" -d '{"users_id": ["ID"], "payload": "Hurakann!", "expiry": 30, "identifier": "I"}' http://api.hurakann/v1/mobile/send
~~~
{: title="cURL" }
