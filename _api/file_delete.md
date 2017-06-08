---
title: /user/file
position: 7
type: delete
description: Removes a file from datastore
---
file_id
: The id for the file previously uploaded 

The file will be removed from datastore
{: .success }

~~~ shell
curl -i -XDELETE -H "Ckey: YOUR_APP_CKEY" -d '{"file_id": "ID"}' http://api.hurakann/v1/user/file
~~~
{: title="cURL" }
