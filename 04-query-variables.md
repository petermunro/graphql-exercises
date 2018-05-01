## Query Variables


Up until now, all our queries have had hardcoded parameters
(eg a `User`s `id`, or the number of objects to fetch
with say `count`).

We really need a way to pass parameters _into_ a query.

This helps us:

1. treat queries as functions that takes parameters, simplifying our thinking; and
2. avoid lots of string building which can potentially degrade performance.

To do this, we set some _query variables_ and then reference them in the query.

1. Start with this query, and execute it:

        organization(login: "facebook") {
            login
            ...orgFields
        }

        fragment orgFields on Organization {
            id
            url
            members {
              totalCount
            }
        }

2. At line 1, add the `query` keyword, an operation name, and a parameter list, so that this:

        {

   becomes this:

        query getOrganization($theId: String!) {

   - We can't omit the `query` keyword when we're using query variables.
   - The parameter name, `theId`, is chosen by us. It is defined at the top of the operation (`$theId: Int!`) and preceded by a `$`.
   - Question: Why did we provide the `!`?

3. Now in GraphiQL, open the `QUERY VARIABLES` pane (bottom left) to specify the query variables to pass in, as JSON:

        {
          "theId": "facebook"
        }

4. GrahiQL will complain that you haven't "used" the query variable, so do so now. Instead of asking for the login `"facebook"`, ask for the login `$theId`.

5. Now execute the query.

6. Notice a few things:

   1. Once defined in the operation, the query variable _must_ be used, and GraphiQL shows a (client-side) error if it isn't.
   2. The type is checked too, so you can't pass in values of the wrong type.
   3. Other errors are checked too, such as providing too many parameters.
   4. All of these checks can be performed client-side, before the query is even sent to the server.

   How much of this checking can REST perform?

7. How are query variables sent to the server?
   Use the browser devtools Network tab to explore.

8. Can you access query variables in a fragment?

9. Can query variables be assigned a default value?
