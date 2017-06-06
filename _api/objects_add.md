---
title: /user
position: 1.5
type: post
description: Create object with custom data
---
branch_id
: The branch id provided along with credentials

profile_id
: The profile id provided along with credentials

The object will automatically stored and indexed into datastore
{: .success }

Create an object into datastore.

~~~ shell
curl -i -XPOST -H "Ckey: YOUR_APP_CKEY" -d '{"branch_id": "asisiud8s", "profile_id": "asdiajd9s8d89s"}' http://api.hurakann/v1/user
~~~
{: title="cURL" }

~~~ erlang
httpc:request(post, "http://api.hurakann.com").
~~~
{: title="Erlang" }
