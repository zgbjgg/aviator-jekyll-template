---
title: /user/login/restore
position: 10
type: get
description: Provides a valid code during next 24 hours to reset object password 
---
email
: The email for the object

Provides a code valid next 24 hours to reset password
{: .success }

~~~json
{
  "code": "WIND"
}
~~~
{: title="Response"}

~~~ shell
curl -i -XGET -H "Ckey: YOUR_APP_CKEY" http://api.hurakann/v1/user/login/restore?email=wind@hurakann.com
~~~
{: title="cURL" }
