---
title: /user/notifications
position: 18
type: get
description: Get a list of notifications or a single one linked to an object 
---
branch_id
: The branch id where the notificatio was linked

notification_id
: The id for the notification previously stored

Get a single notification if provides notification_id, if not return all linked to branch id
{: .success }

~~~json
[
  {
    "title": "A new storm",
    "read": true,
    "notification_id": "ID",
    "time": "10:00",
    "date": "2017-01-01",
    "message": "Welcome to Hurakann"
  }
]
~~~
{: title="Response List"}

~~~json
{
  "title": "A new storm",
  "read": true,
  "notification_id": "ID",
  "time": "10:00",
  "date": "2017-01-01",
  "message": "Welcome to Hurakann"
}
~~~
{: title="Response Single"}

~~~ shell
curl -i -XGET -H "Ckey: YOUR_APP_CKEY" http://api.hurakann/v1/user/notifications?branch_id=ID
~~~
{: title="cURL" }
