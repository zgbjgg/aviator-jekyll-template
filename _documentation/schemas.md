---
title: Schemas
position: 6
---

Schemas are the base to `'mapping'` an entity or object into a backend database, similar to create a table structure in SQL systems. The base for an entity or object (the minimal unity) is the attribute or field, each entity or object has many attributes than can be stored into the whole object, the main characteristic is that each attribute is defined with a set of tools that can define its behaviour in the core and backend system.

Schemas are defined with an XML with a specific structure that the core can parse and store, versioning your entity or object.

When the Schema is uploaded it also translates the entity or object to a RESTful API, so the entity or object can be created, updated or fetched with a specific endpoint defined also in the schema, this is useful because a client can connect and implement this methods instead using the `'RAW'` API exposed by The Hover and have a plus: all data is passed for a serie of validations, so the consistency of each field or attribute is guaranteed by the core instead of implement outside of the box.


#### **_Schema definition_**

The schema must contain the certificates info of your account, so when using the dynamic endpoint you dont need pass this tedious info.

The certificates must include:

- [x] **`name`**: the canonical name of entity or object.
- [x] **`version`**: the version of schema.
- [x] **`user_id`**: the user_id provided along with the certificates.
- [x] **`branch_id`**: the branch_id provided along with the certificates.
- [x] **`profile_id`**: the profile_id provided along with the certificates.

#### **_Attributes_**

Attributes or fields are the minimal unit of an entity or object, and in a schema you can define its behaviour before reach the durability into the backend database.

Each attribute can contain:

- [x] **`name`**: the name of your attribute, this define how your attribute is written in backend database, must start with `'_'`.
- [x] **`required`**: if attribute is required or not when creating the entity, if not provided `'false'` is used.
- [x] **`datatype`**: the datatype of your attribute, the options are: ```boolean, integer, float, date or string```.
- [x] **`indexed`**: if attribute is searchable using `THQL`, default set to false.
- [x] **`length`**: optional, the length of your attribute, must be expressed as an integer value even for integer datatype, if not provided `'unlimited'` is used.
- [x] **`validation`**: optional, a valid regex to run against the attribute value before write or update in backend database.
- [x] **`default`**: optional, if the attribute has a default value when not provided.

#### **_Dynamic Endpoint (RESTful API)_**

Dynamic Endpoint define how the entity or object can be stored, updated or fetched using the rules declared in the attributes section.

The endpoint must contain:

- [x] **`uri`**: the uri to write, update or fetch the entity or object.
- [x] **`methods`**: the methods that can enable the uri, the options are: ```POST, PUT, GET```.
- [x] **`auth`**: the auth method to the uri, the supported for now are: `oauth2` or `none`.

#### **_How to use_**

First to all, you must define a XML containing: definition, attributes and dynamic endpoint, in this example we are using a schema that defines an entity called `post`:

```xml
<schema name="post" version="1.5" user_id="YOUR-USER-ID" branch_id="YOUR-BRANCH-ID" profile_id="YOUR-PROFILE-ID">
  <attributes>
    <attribute datatype="string" name="_title" required="true" length="30" indexed="true" />
    <attribute datatype="string" name="_body" required="true" length="140" indexed="true" />
    <attribute default="0" datatype="integer" name="_likes" required="true" length="3" indexed="true" />
    <attribute datatype="string" name="_date" required="false" length="10" indexed="true" validation="20[1-3][0-9]-[0-1][0-2]-[0-3][0-9]" />
  </attributes>
  <endpoint>
    <uri>/post</uri>
    <methods>POST,PUT,GET</methods>
    <auth>none</auth>
  </endpoint>
</schema>
```

In the above schema we are defining four attributes for the `post` and each attribute has a specific behaviour, also an endpoint is defined in order to access to the write, update or fetch operations.

The next step is upload the schema, so The Hover can parse and create the dynamic endpoint:

```bash
curl -i -XPUT -H "Ckey: YOUR-CKEY" -d @schema_post.xml "http://127.0.0.1:8099/v1/schema"
```

If all goes ok the above request must respond with a 200 OK and then the dynamic endpoint is ready!!.

#### **_Operations_**

##### Storing
Storing method run all validations for each attribute, ensuring that data passed all validations before be written into backend database.
To store an entity/object into the system using your custom defined schema (with the custom endpoint):

```bash
curl -i -XPOST -H "Ckey: YOUR-CKEY" -d '{"_title": "Schemas", "_body": "Hello, I am using schemas", "_likes": 1, "_date": "2016-01-01"}' "http://127.0.0.1:8099/v1/post"
```

##### Updating
Updating method run almost all validations, except for required attributes since in a update the required attributes can be updated or not (not always).
To update an entity/object into the system using your custom defined schema (with the custom endpoint):

```bash
curl -i -XPUT -H "Ckey: YOUR-CKEY" -d '{"_title": "My Schemas", "id": "POST-ID"}' "http://127.0.0.1:8099/v1/post"
```

##### Fetching
To fetch info of an entity/object from the system using your custom defined schema (with the custom endpoint):

```bash
curl -i -XGET -H "Ckey: YOUR-CKEY" "http://127.0.0.1:8099/v1/post?id=POST-ID"
```

#### **_Future Implementations_**

For future works more auth methods can be added to the dynamic endpoints.

