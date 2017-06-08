---
title: /user
position: 2
type: put
description: Update object with custom data into datastore
---
branch_id
: The branch id provided along with credentials

user_id
: The id of the object previously stored

For custom attributes add them starting with a `_` and the name for the attribute. Value of attribute will be determinating automatically based on format
{: .info}

The object will be automatically updated and re-indexed into datastore
{: .success }

~~~ shell
curl -i -XPUT -H "Ckey: YOUR_APP_CKEY" -d '{"branch_id": "YOUR_BRANCH_ID", "user_id": "ID", "_greeting": "hello", "_likes": 10}' http://api.hurakann/v1/user
~~~
{: title="cURL" }
