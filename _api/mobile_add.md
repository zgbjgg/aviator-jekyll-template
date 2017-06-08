---
title: /mobile/register
position: 26
type: post
description: Link an object with a mobile device to send push notifications
---
user_id
: The id of the object previously stored

branch_id
: The branch id of the object previously stored

broot
: The parent branch id of the object

token
: The token of the mobile device

status
: The status of the token, active or inactive

platform
: The platform for the device, can be: android or IOS

Link an object with a mobile device to send push notifications, an object can have multiple devices!
{: .success }

~~~ shell
curl -i -XPOST -H "Ckey: YOUR_APP_CKEY" -d '{"user_id": "ID", "branch_id": "ID", "broot": "ID", "token": "TOKEN", "status": "active", "platform": "IOS"}' http://api.hurakann/v1/mobile/register
~~~
{: title="cURL" }
