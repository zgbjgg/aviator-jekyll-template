---
title: /user/tags
position: 20
type: post
description: Add tags to object into datastore 
---
user_id
: The id for the object previously stored

tags
: The list of tags to be added

Add tags to object into datastore
{: .success }

~~~ shell
curl -i -XPOST -H "Ckey: YOUR_APP_CKEY" -d '{"user_id": "ID", "tags": ["wind", "cold"]}' http://api.hurakann/v1/user/tags
~~~
{: title="cURL" }
