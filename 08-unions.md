## Unions

In GraphQL, the server developer can also use a _union_.

While an interface defines a set of fields, a union defines a set of _other types_ that could be returned.

For example, if Amazon.com had a GraphQL shopping API, when you search they could return a generic `Product` union. But as a concrete type, you could get back a `Book`, a `Television`, a `Grocery` item or something else!

On the server, it could be defined like this:

```
union Product {
  Book | Television | Grocery
}
```

So unions are similar to interfaces. You query for something, and the type system will return an item of the interface or union type, a bit like an abstract type in object-oriented programming.

<!--
1. Run a query in [Github GraphiQL](https://developer.github.com/early-access/graphql/explorer/) to search for `TODO`.

2. How do you know what type is actually returned?

3. Can you add the fields of any of the concrete types to your query?
-->
