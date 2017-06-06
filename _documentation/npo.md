---
title: Nested Procedure Operations
position: 4
---

Nested Procedure Operations (N.P.O) allows executing many operations in a row `step-by-step`, so you won't deal with callbacks from your app. This method avoid inconsistence in data, for example, if you get an object and use the info to update another using your app, maybe external factors such as network connection issues or even programming validations could affect data if some of operations fail before executing the others. 

Hurakann creates a single process to keep the order of steps and execute one by one, if some fails, then the entire operation is applied as `rollback`, otherwise `commit` the transaction.

The N.P.O works using a single interface (API Restful) with a JSON format, and the steps are described based on the web-services in Hurakann API, even you can use a nested procedure into another nested procedure!.

#### **_Features_**

* Many operations in a row `step-by-step`
* Dynamical data injection using `jsonpath`

#### **_How it works?_**

You must define the steps in your procedure, and then model into the JSON request using the `/nested/procedures` endpoint, for example, let's say, we want get an object from the database and then create another object so then a relantionship will be created

First we need to know which one web-service is used for getting info of an object:

| URI | Method | Inject | Request | Next Phase |
|-----|--------|--------|---------|------------|
| user | GET | ```[ {"from": "name", "to": "_parent_name"} ]``` | String Json | Skip |

Now we have our first step, this will look like this:

```json
{
  "uri": "user",
  "method": "GET",
  "inject": [{"from": "name", "to": "_parent_name"}],
  "request":"{\"user_id\":\"id\",\"branch_id\":\"bid\",\"phase\":\"phase1\"}",
  "next": { }
}
```

Now we must design the next step, and in this case the next step use the result of the first step searching the jsonpath equals to `name` and inject in a new attribute of the newly created object using again a jsonpath this time equals to `_parent_name`, so our next step looks like this:

```json
{
  "uri": "user",
  "method": "POST",
  "request":"{
    \"branch_id\":\"bid\",
    \"coloruser\":\"black\",
    \"name\":\"John\",
    \"phase\":\"phase1\",
    \"user_id\":\"id\",
    \"profile_id\":\"pid\",
    \"_parent_name\":\"_\"
  }" 
}
```

if you noticed, the final element of the request is a `_parent_name`, with this in the `to` (inject) we are indicating to the N.P.O that inject the value returned by the first step in this field.

Now putting all together:

```json
{
  "uri": "user",
  "method": "GET",
  "inject": [
    { "from": "name", "to": "_parent_name"}
  ],
  "request": "{
    \"user_id\":\"id\",
    \"branch_id\":\"bid\",
    \"phase\":\"phase1\"
  }",
  "next": {
    "uri": "user",
    "method": "POST",
    "request": "{
      \"branch_id\":\"bid\",
      \"coloruser\":\"black\",
      \"name\":\"John\",
      \"phase\":\"phase1\",
      \"user_id\":\"id\",
      \"profile_id\":\"pid\",
      \"_parent_name\":\"_\"
    }"
  }
}
```

Cool!, now we dont worry about data inconsistence, since all operations all managed by Hurakann and we just use one request to do that!.

#### **_Lexical Rules_**

* The uri is the original URI in the API Restful, but without versioning and if the uri contains more than once slash (`/`), replace this with dot (`.`).
* The Method is the method used by the URI, always must be in uppercase.
* Inject is an array of objects (from, to) with a `jsonpath` of data result, so the jsonpath is evaluated to get the value to send in next step (taken from the result of the actual step). The `from` argument represent the value to search (using jsonpath) in the response of the step. The `to` argument represent the path to replace (using jsonpath) with the new value.
* In the injection of a value, set `_` as the value of the attribute to replace.
* Request is a JSON STRINGIFY of the request body or query-string (if GET Method)
* Next is an object containing the next step, again uri, method, inject, request, and other next step (if any).

#### **_JsonPath_**

`JsonPath` is very similar to the `XPath` in `Xml`, so we use that for a common format of injection data.
If you need more info about how `JSONPATH` works [click here](http://goessner.net/articles/JsonPath/)

You can found the doc for the API [here](http://docs.hoverapi.apiary.io/#reference/nestedprocedures)     

