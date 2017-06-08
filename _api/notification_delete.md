---
title: /user/notifications
position: 17
type: delete
description: Deletes a notification from datastore
---
branch_id
: The branch id where the notificatio was linked

notification_id
: The id for the notification previously stored

Deletes a notification from datastore
{: .success }

~~~ shell
curl -i -XDELETE -H "Ckey: YOUR_APP_CKEY" -d '{"branch_id": "ID", "notification_id": "ID"}' http://api.hurakann/v1/user/notifications
~~~
{: title="cURL" }
