---
title: /user/tags
position: 22
type: put
description: Update tags to object into datastore 
---
user_id
: The id for the object previously stored

tags
: The list of tags to be updated

Update tags to object into datastore
{: .success }

~~~ shell
curl -i -XPUT -H "Ckey: YOUR_APP_CKEY" -d '{"user_id": "ID", "tags": ["wind", "cold"]}' http://api.hurakann/v1/user/tags
~~~
{: title="cURL" }
