---
title: /user/file
position: 6
type: post
description: Upload a file into datastore
---
multipart/form-data
: The file in a multipart form-data format

The file will be stored into datastore and return its id
{: .success }

~~~json
{
  "file_id": "ID"
}
~~~
{: title="Response"}

~~~ shell
curl -i -XPOST -H "Ckey: YOUR_APP_CKEY" -H "Content-Type: multipart/form-data" -F "file=@storm.png" http://api.hurakann/v1/user/file
~~~
{: title="cURL" }
