---
title: /user/tags
position: 23
type: get
description: Get tags of object from datastore 
---
user_id
: The id for the object previously stored

Get tags of object from datastore
{: .success }

~~~json
{
  "tags": ["wind", "storm"]
}
~~~
{: title="Response" }

~~~ shell
curl -i -XGET -H "Ckey: YOUR_APP_CKEY" http://api.hurakann/v1/user/tags?user_id=ID
~~~
{: title="cURL" }
