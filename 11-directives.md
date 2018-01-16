## Directives

Suppose you want to alter your query depending on the state of a variable. _Directives_ offer a way to do this, or to otherwise configure how your query is executed.

Directives start with an `@` sign then a keyword, and can have arguments. Two are currently defined in the GraphQL spec: `@include` and `@skip`, but more are likely to appear in future versions.

1. First, in [Github GraphiQL](https://developer.github.com/early-access/graphql/explorer/), create a query to search for an `organization` (eg `shopify` or `microsoft`), and retrieve its `id`, `login`, `name` and `projectsUrl` fields.

2. Now alter your query to retrieve the `name` and `projectsUrl` only if a specific query variable is true. To do this:

   1. Inside the query, use an inline fragment to retrieve the `name` and `projectsUrl` data.

   2. Modify your inline fragment: after the `...` spread operator, add the `@include` directive. This takes an `if:` argument, so the relevant line looks like this:

      ```
      ... @include(if: true) {
      ```

      In other words, this says "only fetch the fields inside the fragment if the following value is true". Verify that this produces the same result as the previous step.

    3. Change the value to false, rerun the query, and ensure that the fields are _not_ retrieved this time.

    4. Now replace the `false` value with a query variable, and test again for both `true` and `false`. Verify that changing the query variable alters the query and the fields retrieved.

  3. Modify the query to use `@skip`. What happens?

  4. Does the GraphQL syntax allow for multiple directives on the same line for the same inline fragment?

  5. Where are the directives interpreted - client or server? What gets sent across the wire in each direction?
