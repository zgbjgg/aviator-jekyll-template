---
title: /user/search/ql
position: 19
type: get
description: Executes a HQL search into datastore
---
branch_id
: The branch id of the tree level

thql
: The query to execute, see HQL for more info

pagination
: The number of rows for page

page
: The page to return, only when using pagination

pagination_id
: The pagination id, only when using pagination

In the users array are the resultset, all INCLUDE field should be placed here
{: .info}

Executes a HQL query into datastore, page and pagination must be sent when walk into pages
{: .success }

~~~json
{
  "total_results": 100,
  "pagination_id": "ID",
  "pages": 10,
  "users": [
    {
      "user_id": "ID",
      "profile_id": "ID",
      "phase": "phase1",
      "merge": "main",
      "broot": "ID"
    }
  }
}
~~~
{: title="Response"}

~~~ shell
curl -i -XGET -H "Ckey: YOUR_APP_CKEY" http://api.hurakann/v1/user/notifications?branch_id=ID&pagination=10&thql=WHERE name:s=Hurakann
~~~
{: title="cURL" }
