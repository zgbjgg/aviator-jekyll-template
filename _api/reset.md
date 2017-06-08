---
title: /user/login/reset
position: 11
type: post
description: Reset object password using a valid code 
---
email
: The email for the object

new_password
: The new password for the object

code
: The code previously generated with restore api

Reset the object password using a valid code
{: .success }

~~~ shell
curl -i -XPOST -H "Ckey: YOUR_APP_CKEY" -d '{"email": "wind@hurakann.com", "new_password": "WIND", "code": "STORM"}' http://api.hurakann/v1/user/login/reset
~~~
{: title="cURL" }
