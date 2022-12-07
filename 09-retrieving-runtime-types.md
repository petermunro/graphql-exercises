## Retrieving Runtime Types

1. On the [Github API](https://developer.github.com/early-access/graphql/explorer/), try running a query like this. Should it execute?

   ```
   {
     node(id: "U_kgDOAAi8FQ") {
       id
       __typename
       login
       name
     }
   }
   ```

2. We asked for an interface type (`Node`), and even though it may have returned a `User`, we can't retrieve that User's `login` or `name`, because they're not defined on `Node`, the interface type.

   To include fields based on their runtime type, we can use _fragments_.

3. Create a fragment to query the `login` and `name` fields, and then 'call' it from your query using the spread operator. What happens?

4. Run the same query and fragment again, but with a different `id` (eg `O_kgDOAA3wnw`) that retrieves a different type. What response do you get? Do you get an error?

5. How could you retrieve a `login` and `name` if a `User` is returned, but a `description`, `name` and `location` if an `Organization` is returned? Try it.
