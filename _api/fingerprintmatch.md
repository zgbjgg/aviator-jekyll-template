---
title: /match/fingerprint
position: 25
type: get
description: Compare two fingerprints and check if match
---
fmd_right
: The right fingerprint in base64

fmd_left
: The left fingerprint in base64

Fingerprints base64 must be in format `ISO-19794-2-2005`
{: .info}

Compare two fingerprints and check if they match or not
{: .success }

~~~ shell
curl -i -XGET -H "Ckey: YOUR_APP_CKEY" http://api.hurakann/v1/match/fingerprint?fmd_left=BASE64&fmd_right=BASE64
~~~
{: title="cURL" }
