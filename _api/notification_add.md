---
title: /user/notifications
position: 16
type: post
description: Creates a notification linked to an object or its tree into datastore 
---
title
: The title for the notification

message
: The body for the notification

broot
: The branch id of the object to send notification to all its objects under its branch

branch_id
: The branch id of the object to link directly the notification

Creates a notification for a complete tree or single linked to an object
{: .success }

~~~ shell
curl -i -XGET -H "Ckey: YOUR_APP_CKEY" -d '{"title": "Welcome", "message": "This is Hurakann", "branch_id": "ID"}' http://api.hurakann/v1/user/notifications
~~~
{: title="cURL" }
