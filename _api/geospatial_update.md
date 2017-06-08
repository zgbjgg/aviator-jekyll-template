---
title: /v1/geospatial
position: 29
type: put
description: Re-index a location into geospatial datastore
---
latitude
: The latitude for the location

longitude
: The longitude for the location

id
: The id of the object previously stored into geospatial datastore

name
: An optional name for the location in geospatial datastore

Re-index a location into geospatial datastore
{: .success }

~~~ shell
curl -i -XPOST -H "Ckey: YOUR_APP_CKEY" -d '{"latitude": "0", "longitude": "0", "id": "ID", "name": "Wind"}' http://api.hurakann/v1/geospatial
~~~
{: title="cURL" }
