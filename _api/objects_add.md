---
title: /user
position: 1
type: post
description: Create object with custom data into datastore
---
branch_id
: The branch id provided along with credentials

profile_id
: The profile id provided along with credentials

user_id
: The user id provided along with credentials

coloruser
: The color of the object, `black` objects cannot create a tree below them, `blue` can do it.

phase
: The phase for the object. Default to `phase1`.

password
: The password for the object (used login service).

name
: The name for the object. This value is set for default purposes and you can use it in your own way.

email
: The email for the object (used in login service)

username
: The username for the object (used in login service)

latitude
: If object is a location

longitude
: If object is a location

lastname
: The lastname for the object. This value is set for default purposes and you can use it in your own way.

lastname2
: The lastname2 for the object. This value is set for default purposes and you can use it in your own way.

For custom attributes add them starting with a `_` and the name for the attribute. Value of attribute will be determinating automatically based on format
{: .info}

The object will be automatically stored and indexed into datastore
{: .success }

~~~ shell
curl -i -XPOST -H "Ckey: YOUR_APP_CKEY" -d '{"branch_id": "YOUR_BRANCH_ID", "profile_id": "YOUR_PROFILE_ID", "user_id": "YOUR_USER_ID", "coloruser": "black", "phase": "phase1", "_greeting": "hello", "_likes": 10}' http://api.hurakann/v1/user
~~~
{: title="cURL" }
