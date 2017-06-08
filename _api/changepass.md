---
title: /user/login/change_password
position: 12
type: put
description: Change the object password with a new one 
---
user_id
: The id for the object previously stored

old_password
: The old password for the object

new_password
: The new password for the object

Change the object password with a new one into datastore
{: .success }

~~~ shell
curl -i -XPUT -H "Ckey: YOUR_APP_CKEY" -d '{"user_id": "ID", "old_password": "STORM", "new_password": "WIND"}' http://api.hurakann/v1/user/login/change_password
~~~
{: title="cURL" }
