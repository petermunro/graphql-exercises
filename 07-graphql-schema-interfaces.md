## Interfaces

In GraphQL, the server developer can use an _interface_, which defines
a set of fields.

For example, you could have a `Name` interface defined on the server like this:

```
interface Name {
  firstName: String!
  lastName: String!
}
```

Any type that _implements_ that interface _must include_ those exact fields with the same types.

In a request, you can ask for a field that is of an interface type:

1. In the [Github GraphiQL](https://developer.github.com/early-access/graphql/explorer/), ask for a `node` field with an `id` of:

   `MDQ6VXNlcjU3MjQzNw==`.

   This field has subfields, so ask for the `id` subfield.

2. How many subfields does the `Node` interface have?

3. How many non-scalar types are there on this server (approximately)?
   Use GraphiQL's Documentation Explorer to drill down from
   the top-level `Query` type.

4. Which of these types implement the `Node` interface? To find
   out, navigate to `Node` and look at the list of types
   implementing it.

5. So if you request a data item of type `Node`, how many different types _could_ you potentially receive? What are some example types?

6. Can you add the fields of any of those concrete types to your query?
