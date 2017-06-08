---
title: /geospatial
position: 30
type: get
description: Search locations near of a given point into geospatial datastore 
---
lat
: The latitude for the location

lon
: The longitude for the location

d
: The distance from the given point (in km)

max
: The max resultset of locations near of given point

Search locations near of a given point into geospatial datastore
{: .success }

~~~json
{
  "geos": [
    {
      "km": 10.4,
      "id": "ID",
      "name": "Wind Avenue"
    } 
  ]
}
~~~

~~~ shell
curl -i -XGET -H "Ckey: YOUR_APP_CKEY" http://api.hurakann/v1/geospatial?lat=0&lon=0&max=10&d=10
~~~
{: title="cURL" }
