---
title: /user/file
position: 8
type: get
description: Download a file from datastore
---
file_id
: The id for the file previously uploaded 

The file will be downloaded from datastore with a custom mime type
{: .success }

~~~ shell
curl -i -XGET -H "Ckey: YOUR_APP_CKEY" http://api.hurakann/v1/user/file?file_id=ID
~~~
{: title="cURL" }
