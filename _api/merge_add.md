---
title: /user/merge
position: 13
type: post
description: Merges two or more objects into a collection
---
branch_id
: The branch id of the main object

main_user_id
: The id of the main object in the collection

users_id
: The ids of the objects to be set into collection

Merge two or more objects into a collection and set an object as the main of the collection
{: .success }

~~~ shell
curl -i -XPOST -H "Ckey: YOUR_APP_CKEY" -d '{"branch_id": "ID", "main_user_id": "ID", users_id: ["ID", "ID"]}' http://api.hurakann/v1/user/merge
~~~
{: title="cURL" }
