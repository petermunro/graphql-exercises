# Extending the Server Schema

In this module, we will extend the "hello world" schema with a new type and a new top-level query field.

## Refactoring into Separate Files

1. At the moment, the server exists in a single file.
   It would be worth refactoring this into separate files:
   one for the schema, another for the resolvers, and have these
   `require`d from the main server file.

## Adding a `Person` Type

1. I'd like to be able to query a `Person`, like this:

        {
          person(id: "14") {
            firstName
            lastName
            city
            country
            id
          }
        }

   To do this, we will:

      1. add a new `Person` type to our schema; and
      2. add a resolver to return some data.

2. Add the `Person` type:
   - Make `firstName` and `lastName` required fields (`String!`).
   - Add an `id` field of type `ID`, and make this required too.
   - Change the top-level Query field from `hello: String` to `person(id: ID!): Person`. This means we can ask for the `person(id: "14")` field, and this will return a `Person`.


3. Now to update the resolvers. Currently the map looks like this:

        var resolvers = {
          Query: {
            hello(root) {
              return 'world';
            }
          }
        };

   We want a field `person` which returns a Person object.
   For the moment, hard code a return object, ignoring the input `id`. Simply returning a JavaScript object of the same "shape" is enough.

4. Restart your server, and issue the query.
