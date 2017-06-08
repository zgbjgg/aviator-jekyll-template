---
title: /user
position: 3
type: get
description: Get object with custom data from datastore
---
branch_id
: The branch id provided along with credentials

user_id
: The user id for the object previously stored

phase
: The phase for the object, can be `phase1` or `all`.

The response contains the object previously stored with custom data from datastore
{: .success }

~~~json
{
  "user": {
    "branch_id": "ID"
  },
  "profile": {
    "name": "PROVISIONING-PROFILE-APP",
    "profile_id": "YOUR_PROFILE_ID"
  },
  "phase": "phase1",
  "created_at": "2017-03-09T00:00:00Z",
  "updated_at": "2017-03-09T00:00:00Z",
  "fmd": false,
  "greeting": "hello",
  "likes": 10
}
~~~
{: title="Response"}

~~~ shell
curl -i -XGET -H "Ckey: YOUR_APP_CKEY" http://api.hurakann/v1/user?branch_id=YOUR_BRANCH_ID&user_id=ID&phase=all
~~~
{: title="cURL" }
