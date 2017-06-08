---
title: /user/is_color
position: 5
type: get
description: Check if an object is the color requested from datastore
---
user_id
: The id of the object previously stored

color
: The color to check, can be: `blue` or `black`

If object is in the color requested return its branch id
{: .success }

~~~json
{
  "branch_id": "ID"
}
~~~
{: title="Response"}

~~~ shell
curl -i -XGET -H "Ckey: YOUR_APP_CKEY" http://api.hurakann/v1/user/is_color?user_id=ID&color=black
~~~
{: title="cURL" }
