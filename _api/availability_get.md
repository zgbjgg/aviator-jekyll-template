---
title: /user/availability
position: 4
type: get
description: Check the existence of an object into datastore
---
identity
: The attribute to eval, can be: an email or username of an object previously stored

If response code is 200 object exists in datastore otherwise 404 is returned. 
{: .success }

~~~ shell
curl -i -XGET -H "Ckey: YOUR_APP_CKEY" http://api.hurakann/v1/user/availability?identity=wind@hurakann.com
~~~
{: title="cURL" }
