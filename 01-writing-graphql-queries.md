
## Writing GraphQL Queries

To learn GraphQL, we'll start by using the GitHub API.

1. Sign in to GitHub (get a GitHub username if you need one).
   Go to the GitHub [GraphQL Explorer](https://developer.github.com/early-access/graphql/explorer/).

2. You can now execute GraphQL queries in this tool, called _GraphiQL_.

   1. Queries look like one of:

      Operation | Description
      ---|---
      `query { foo }`           | An unnamed query
      `{ foo }`                 | An unnamed query - shorthand form
      `query MyQuery { foo }`   | A named query

   2. We'll just use the shorthand form for now.
      In the left pane type an open brace `{`: you'll see GraphiQL complete the query by adding the closing brace.
      Hit return.

   3. With the cursor between the braces, type CTRL-SPACE to view a list of completions. Select `viewer`. This reflects data about the current viewer of the graph (you).

   4. Add an open brace and hit RETURN. Add the following fields:

      - login
      - avatarURL
      - createdAt
      - id
      - isViewer    

      Execute the query (shortcut: CTRL-RETURN or CMD-RETURN).

      Your query should look like this:

          viewer {
            login
            createdAt
            id
            isViewer    
          }

   5. A hint: Hovering over a red underline presents an error message.

   6. A brief look at query syntax. Investigate the following:

      1. Do the fields need to be on separate lines, or is a space enough to separate them?
      2. Can you add commas between fields if necessary?
      3. Does ordering of fields matter?
      4. What happens if you repeat a field name?
      5. Does adding the word `query` before the top-level opening brace change anything?
      6. Make it a named query. Can you specify multiple named queries, and if so, which one gets executed? Does the "Execute Query" button let you choose?
      7. In these exercises (and typically), you'll send just one query at a time, so when sending a new query, just overwrite a previous one in the GraphiQL tool.

### Field Parameters

   1. Fields may take parameters (depending on how the schema was defined). Perform a new query for the `repository` owned by `graphql` and identified by the name `graphql-js`. To do this, after `repository`, type a `(` and use command completion to see the options. Then enter a `:` and the parameter value in double quotes. retrieve the `description`, `id` and `createdAt` fields.


### Nested Queries

In GraphQL, most queries are made up of a set of _fields_ that form a _selection set_. A field represents a simple value such as a string or an integer.

Fields can also represent more complex data, or relationships to other data, in which case they too will have subfields. This nesting can continue indefinitely.

Ultimately, all selections must resolve to simple fields which return scalar values.

   1. Add in the following to your repository query, underneath the `createdAt` field:

                commitComments(first: 5) {
                  edges {
                    node {
                      author {
                        login
                      }
                      body
                    }
                  }
                }

      What does this query find?

    2. Use the top-level field `organization` to retrieve in one response, for "facebook":

       - its login
       - the total count of its members
       - when the repository called "relay" was created


3. What are the _top level_ queries that may be run? To find out, remove everything except `{ }` and type CTRL-SPACE between the braces.

4. Examine the "Docs" button to the right. It enables you to browse the schema.
     - Under "Docs", navigate to the ROOT TYPE: `query: Root`.
     - You'll see a list of fields.

   How do types relate to fields?
