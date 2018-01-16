
## Introspecting the Schema

> How does _GraphiQL_ type check your query before you've even sent it?

- In fact, _any_ client needs to check the query before sending to the server.

To do this, a client can send an _introspection query_. This asks "which types and fields do you have"? This is also how _GraphiQL_ populates the right-hand side _Docs_ pane.

You can query against the GraphQL schema yourself. Paste this query into the left pane:


    {
        __schema {
            queryType {
                name
                fields {
                    name
                    description
                }
            }
        }
    }


  1. Does the Github API define any enumerated types?

  2. Within the `fields` field, what does the `args` field contain?
