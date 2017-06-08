---
title: /fingerprint/verify
position: 24
type: get
description: Check if provided fingerprint match the fingerprints of object into datastore
---
user_id
: The id for the object previously stored

id
: The fingerprint in base64

Fingerprint base64 must be in format `ISO-19794-2-2005`
{: .info}

Check if provided fingerprint match the fingerprints stored
{: .success }

~~~ shell
curl -i -XGET -H "Ckey: YOUR_APP_CKEY" http://api.hurakann/v1/fingerprint/verify?user_id=ID&id=BASE64
~~~
{: title="cURL" }
