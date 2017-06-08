---
title: /user/merge
position: 15
type: get
description: Get objects from merged collection
---
user_id
: The id of the main object in the collection

Gets merged collection using the main object 
{: .success }

~~~json
[
  {
    "user_id": "ID",
    "name": "NAME_IF_SET",
    "merge": "main"
  },
  {
    "user_id": "ID",
    "name": "NAME_IF_SET",
    "merge": "merge"
  }
]
~~~
{: title="Response" }

~~~ shell
curl -i -XGET -H "Ckey: YOUR_APP_CKEY" http://api.hurakann/v1/user/merge?user_id=ID
~~~
{: title="cURL" }
