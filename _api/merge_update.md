---
title: /user/merge
position: 14
type: put
description: Update objects in merged collection
---
branch_id
: The branch id of the main object

main_user_id
: The id of the main object in the collection

users_id
: The ids of the objects to be set into collection

new_main_user_id
: The id of the new main object in the collection

Updates merged collection and set an object as the main of the collection
{: .success }

~~~ shell
curl -i -XPUT -H "Ckey: YOUR_APP_CKEY" -d '{"branch_id": "ID", "main_user_id": "ID", users_id: ["ID", "ID"], "new_main_user_id": "ID"}' http://api.hurakann/v1/user/merge
~~~
{: title="cURL" }
