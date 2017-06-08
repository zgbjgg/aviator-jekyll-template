---
title: /user/login
position: 9
type: get
description: Executes a login of an object from datastore 
---
user
: The key for the object, can be: email or username

password
: The password for the object 

Performs the login action and return the results
{: .success }

~~~json
{
  "user_id": "ID",
  "name": "NAME_IF_SET",
  "lastname": "LASTNAME_IF_SET",
  "lastname2": "LASTNAME2_IF_SET",
  "branch_id": "ID"
}
~~~
{: title="Response"}

~~~ shell
curl -i -XGET -H "Ckey: YOUR_APP_CKEY" http://api.hurakann/v1/user/login?user=wind@hurakann.com&password=storm
~~~
{: title="cURL" }
