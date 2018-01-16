
## Inline Fragments

Having to define new fragments to retrieve fields of concrete types can be a little unwieldy. To make things simpler, you can create _inline fragments_ which are defined and used within the query itself.

To do this, use the spread operator and define the fragment at point of use, omitting the word `fragment` and its name. So this:

```
{
  node(id: "3") {
    id
    ...nameFields
  }
}

fragment nameFields on Person {
  firstName
}
```

…becomes this:

```
{
  node(id: "3") {
    id
    ...on Person {
      firstName
    }

  }
}
```

1. Using inline fragments, retrieve the fields for two different concrete types from a result. (TODO: which ones?)

2. You can think of the `...on Person` as a "type condition". If a `Person` is returned, its fields (eg `firstName`) will be retrieved. So you can select the fields you want based on the runtime type, kind of like a declarative `if` statement: if a `Person` is returned, get me their `firstName`.

3. If the fields in the inline fragment are of the same type as the enclosing context, you can omit the `on MyType`. What does this query return?

    ```
    {
      location(id: 4) {
        name
        address
        ... {
          city
          country
        }
      }
    }
    ```

   This may not seem that useful, but its use will become clear in the next module.
