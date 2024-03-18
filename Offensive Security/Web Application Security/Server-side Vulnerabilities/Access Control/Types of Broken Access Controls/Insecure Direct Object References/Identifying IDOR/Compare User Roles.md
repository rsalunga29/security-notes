In some advanced cases, we may need to register multiple accounts and compare their HTTP requests and object references, which may allow us to understand how the URL parameters and unique identifiers are being calculated and then calculate them for other users to gather their data.

For example, one of our users can view their salary after making the following API call.
```http
GET /profile HTTP/1.1
...

{
  "attributes" : 
    {
      "type" : "salary",
      "url" : "/services/data/salaries/users/1"
    },
  "Id" : "1",
  "Name" : "User1"

}
```
The second user may not have all of these API parameters