---
title: GeoSpatial - Search points using GPS
position: 5
---

GeoSpatial allows you store (index) and update `"locations"` in your database segment to use for searching and calculating distances from locations stored to a single given point.

Imagine that you want implement a system to geo-referencing your users (for example, retail or proximity cases), so when some of your users (using a device), provide their location (latitude and longitude) and then you perform a search into your database to search the nearest location (previously registered) and The Hover answers with a resultset with that locations.

#### **_Use case_**

For example, we saved this locations in our database using the API `geospatial`:

```
	Location Store One: 18.956952,-99.2315226
	Location Store Two: 18.9613766,-99.2344753
	Location Store Three: 18.63222,-99.1615037
```

Now one of our users provide his location with a point nearest of the location `Location Store One` then, sending that with the `geospatial GET` you should receive a resultset, ordered from the location nearest:

```json
{"geos":
  [
    {"km":0.13275527391449998,"id":"IDLOCONE","name":"Location Store One"},
    {"km":0.4584615115187,"id":"IDLOCTWO","name":"Location Store Two"},
    {"km":36.955166644128,"id":"IDLOCTHREE","name":"Location Store Three"}
  ]
}
```

Let's analyze the results, as you can see, the nearest location is `Location Store One` since it is `0.1327` Km away, and the other locations are away from the user actual location.

You can found the doc for the API [here](http://docs.hoverapi.apiary.io/#reference/geospatial)     
