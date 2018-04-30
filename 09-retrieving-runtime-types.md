## Retrieving Runtime Types

1. On the [Github API](https://developer.github.com/early-access/graphql/explorer/), try running a query like this. Should it execute?

   ```
   {
     node(id: "MDQ6VXNlcjU3MjQzNw==") {
       id
       __typename
       login
     }
   }
   ```

2. We asked for an interface type (`Node`), and even though it may have returned a `Person`, we can't retrieve that Person's `firstName`, because it's not defined on `Node`, the interface type.

   To include fields based on their runtime type, we can use _fragments_.

3. Create a fragment to query the `name` field, and then 'call' it from your query using the spread operator. What happens?

4. Run the same query and fragment again, but with a different `id` (eg `MDEyOk9yZ2FuaXphdGlvbjkxMzU2Nw==`) that retrieves a different type. What response do you get? Do you get an error?

5. How could you retrieve a `firstName` if a `Person` is returned, but a `homeTown` if a `Meet` is returned? Try it.
