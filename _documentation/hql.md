---
title: HQL
position: 3
---

With HQL you can query (search) over your stored and indexed objects into your database segment.
HQL has many features to satisfy the most common search cases in a common system. HQL is inspired and based in `Solr` queries but with a powerful model that has many differences from the original.

In difference to other QL (Query Languages), HQL uses a specific syntax and commands to retrieve data.
Hurakann can interpret your query from a single line of code as in SQL SELECT, 
but without specifiying the SELECT and FROM on the same query, just over your entity.

In the last version of HQL you must provide the `datatype` to each field in the query, so, if you save your object with some field as int, boolean or string, just provide that info to the query:

```sql
WHERE name:s=Allison AND years:i=40 
```

The datatype must be after `':'`. The supported datatypes are: 

| Prefix | Datatype |
--------|----------|
| i     | integer  |
| s     | string   |
| b     | boolean  |
| f     | float    |
| dt    | date     |

*date* type must be in format **ISO 8601**
{: .info}

Let's do it!

#### **_Simple Querying_**

For example, in our database we saved our object whit name, lastname and also a custom parameters called _box_id, _years and _company_id, then our object looks like this:

```json
{
  "name":"Allison",
  "lastname":"Mosshart",
  "_box_id":"1AB456",
  "_years":40,
  "_company_id":"1abcb718ajcnakaks819"
}
```

Now, how we can search all objects with 'Allison' in the field name?, simple, in the search API use HQL:

```sql
WHERE name:s=Allison
```

HQL uses AND, OR, NOT condition to satisfy logic operators, for example, search the objects with name 'Allison'
or with name 'Jack' but NOT name 'Meg':

```sql
WHERE name:s=Allison OR name:s=Jack NOT name:s=Meg
```

#### **_Wildcard_**

You can use the wildcard * to match everything after or before a string comparison, example, search the objects that name starts with 'Jac' like 'Jack', 'Jackie':

```sql
WHERE name:s=Jac*
```

#### **_Ranges_**

You can use ranges on fields that are numeric fields, for example, search the objects with years mayor than 30 and
minor than 50:

```sql
WHERE years:i<50 AND years:i>30
```

Ranges apply for datatypes: `float, integer and date`.

Ranges must be set with mayor and minor, for that purpose use wildcard * if one of limits are not provided, example, search years only mayor to 50:
{: .info}

```sql
WHERE years:i<* AND years:i>50
```

#### **_Time Series_**

In every object stored in the database there are two attributes indexed by default: `inserted_at` and `updated_at`. The timestamp is useful when you want retrieve objects in a range of time so for example you can query data from the first of this month until today (updated or inserted). In order to execute the query in a successful state the date must be converted to _ISO 8601_:

```sql
WHERE inserted_at:dt>2017-03-09T00:00:00Z AND inserted_at:dt<2017-03-13T00:00:00Z...	
```

If you noticed the date is passed in **ISO 8601** format, so in the example the query will retrieve all objects created between 2017-March-09 and 2017-March-13.
          
#### **_Grouping_**

When you perform a complex search maybe grouping data could be useful, example, search the objects with name 'Allison' or Jack and box_id that starts with 'ABC':

```sql
WHERE (name:s=Allison OR name:s=Jack) AND box_id:s=ABC*
```

Grouped data are enclosed into parentheses ( ). HQL only allows one group at time, no group into group

#### **_Included Fields_**

Included fields is a feature of HQL to retrieve specific fields of a object in a search, example, search the objects with name 'Allison' and include on each result the years:

```sql
WHERE name:s=Allison INCLUDE years
```

For more included fields, just separate with ',' delimiter
{: .info}

#### **_Parent Fields_**

When you create your object, any of your custom fields could have an id of another object inside (like a link), then in your search you want to know the parent object fields, example, search the objects with name 'Allison' and include on each result the years, also retrieve the name of the company that belongs the object:

```sql
WHERE name:s=Allison INCLUDE years PARENT_FIELDS company_id
```

For more parent fields, just separate with ',' delimiter
{: .info}

HQL just retrieve parent fields from the actual object, just for one level
{: .error}
	
Then on each object you can extract the tag 'company_id_obj' that is the object representing the company,
similar to make a GET request. To extract the PARENT_FIELDS result from each object just concat to your field the prefix 'obj', so in the example we set PARENT_FIELDS with company_id, then extract company_id_obj

#### **_Sorting_**

With HQL you can sort your query results in ascendent or descendent form. To use this just use SORT_BY_ASC (for ascendent) or SORT_BY_DESC (for descendent) and the field that you want sort by, example, search the objects where name starts with Jac and then sort by name in ascendent form:

```sql
WHERE name:s=Jac* SORT_BY_ASC name_s
```

You must set a valid field to sort by, the field must follow by the type of it, for example if your field is string, then: name_s, if it's integer: name_i or if it's boolean: name_b.
{: .info}

#### **_AS LINK_**

The new version of HQL now support the `LINK` operation and it's very simple to use, since it works like a `JOIN` in SQL systems. The `LINK` operation can be used when you want query your objects with a relationship between them in only one query (in one sentence), so for example, this allows you query data from different objects and link them to generate only one output.

Example: imagine a system that a user can publish posts (in a blog), then each post is a single object in the database and the users publishing are other objects in the same system, then, how we can query the posts from the user with the nickname equals to `almoss`?, simple, use `LINK`:

```sql
WHERE nickname=almoss AS user LINK entity=post AND owner=user.id INCLUDE favs,text
```

Explaining the query: HQL evaluates the first query that is: **`nickname=almoss`**, then retrieve objects from database where the condition is true, so the result of this query is stored in a variable called `user`, and linked to another query searching the objects where entity equals to `post` and owner equals to id of the variable `user`.

The `id` in the alias is the id of the objects (when saving post, each of them have an owner attribute with the id of the user), but however you can use the attributes of the objects queried and assigned to the alias, for example, if our user has an attribute `age`, then we can use `user.age` to insert the value of the attribute using the alias.

The alias always have an attribute id that is the id of the object in the system.
{: .info}

#### **_Regular Expressions_**

As in `solr v4` the `HQL` supports regular expressions in queries, only in string fields, for example:

```sql
WHERE name:s=/.*[Mm]egan.*/
```

The above query will search over objects where the string `Megan` or `megan` is present somewhere in the field.
If you need more info about how to use and examples how to use regular expression consult [this tutorial](http://www.openjems.com/solr-regex-tutorial/).


#### **_HQL BIFs (built-in functions)_**

HQL also supports a feature called `BIFs` that is a built-in functions in the backend system, the built-in functions need a function declared over a field followed by a query and returns a single response instead many records as the common searches. The next are the `BIFs` supported for now:

| BIF | Description| 
|-----|---------|
| MAX | Returns the max value of a rows|
| MIN | Returns the min value of a rows|
| AVG | Returns the average of a rows (for a field)|
| SUM | Returns the sum of a rows (for a field)|

For example, let's say we want to know the total likes of all user's posts, then to perform that we must use the `SUM` BIF:

```sql
SUM likes:i WHERE entity=post AND nickname:s=Allison
```

The above query could return the sum of all likes: ```json {"sum": 5004}```

Another good example could be if we want to know the age of the older employee and the average of all ages of all employees:

```sql
MAX years:i WHERE name:s=* AND type:s=employee
```
```sql 
AVG years:i WHERE name:s=* AND type:s=employee
```
The result of each BIF is a single json with one attribute, containing the name of the BIF as key and the value will be the numeric result. Each BIF must be sent with a single field and the field must contains the prefix for datataype.

#### **_Restrictions_**

* A query could start with reserved words for a `BIF`: `MAX`, `MIN`, `AVG`, `SUM`
* A query could start with reserved word `WHERE`
* In a query, if not provide sort field, default is set to `name`
* All fields must contains datatype, if not provided then `s` is used.
* Conditions must be separated by spaces
* `OR`, `AND`, `NOT` are reserved words and must be used in uppercase
* `PARENT_FIELDS` and `INCLUDE` are reserved words and must be used in uppercase
* For many fields on `INCLUDE` or `PARENT_FIELDS` use comma as delimiter
* For `SORT_BY_DESC` and `SORT_BY_ASC` field must have a prefix of data type
* For `AS _ LINK` the sentence must start with `AS`, after a var and finish with a `LINK`, then other query
* Allowed operators are: `=`, `>`, `<`, `<=`, `>=`
