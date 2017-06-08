---
title: /mobile/register
position: 26
type: put
description: Update the status of token mobile device to send push notifications
---
user_id
: The id of the object previously stored

token
: The token of the mobile device

status
: The status of the token, active or inactive

Update the status of token mobile device to send push notifications
{: .success }

~~~ shell
curl -i -XPUT -H "Ckey: YOUR_APP_CKEY" -d '{"user_id": "ID", "token": "TOKEN", "status": "active"}' http://api.hurakann/v1/mobile/register
~~~
{: title="cURL" }
