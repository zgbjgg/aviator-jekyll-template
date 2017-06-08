---
title: /user/notifications
position: 16
type: put
description: Mark as read or unread the notification
---
notification_id
: The id for the notification previously stored

read
: The status of the read, true or false

Mark the notification read or not into datastore
{: .success }

~~~ shell
curl -i -XPUT -H "Ckey: YOUR_APP_CKEY" -d '{"notification_id": "ID", "read": true}' http://api.hurakann/v1/user/notifications
~~~
{: title="cURL" }
