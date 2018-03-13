## Fragment Matcher

### The Symptom

You may have seen a lot of console error messages such as:

    WARNING: heuristic fragment matching going on!

    Missing field temperature in {
      "id": "1",
      "name": "Hall Light",
      "brightnessLevel": 100,
      "manufacturer": "Philips",
      ...


### Background to Apollo Caching

Apollo Client tries to store correct object data in its cache. In other words, each cached object contains fields which match the schema.

But by default, Apollo Client doesn't _have_ access to the schema! This is so it can work easily out of the box.

For most cases, this lack of checking against the schema works fine. Apollo Client just places the returned data into the cache against the object's type and id.

### Fragments on Interfaces

But when you use fragments on interfaces (or unions), that throws a spanner into the works. Apollo Client can make a guess as to which fields belong to which type using its _Heuristic Fragment Matcher_, but it's not perfect.


Think about a query like this:

    {
      accessories(offset: 0, limit: 5) {
        id
        name
        ... on Light {
          brightnessLevel
          manufacturer
        }

        ... on Thermostat {
          temperature
        }
      }
    }

How will Apollo Client know whether the Accessory retrieved should contain _all_ the fields across _all_ the fragments, or just some of them?

In other words, regardless of the fragment names (which have meaning only to humans), how does it know the relationships between these types? A Thermostat could be a Light could be an Accessory, for all it knows, in which case it would need every field in every fragment.

### Solution

A solution to this is to give Apollo Client the schema it needs.

1. Create a file in the top level of your homehub client project, calling it `getFragmentSchema.js`.
Place the code from [here](https://gist.github.com/petermunro/28b2231d0b8d688011f6265f6d094913) into it.

2. Run this code:

        $ node getFragmentSchema.js

   It should retrieve the types and their relationships from your server into a JSON file and place it into `src/fragmentTypes.json`.

3. Modify `src/index.js`, inserting this code:

        import { IntrospectionFragmentMatcher } from 'apollo-cache-inmemory';
        import introspectionQueryResultData from './fragmentTypes.json';

        const fragmentMatcher = new IntrospectionFragmentMatcher({
          introspectionQueryResultData
        });


4. Modify the `cache` line where you instantiate a new ApolloClient, inserting `{ fragmentMatcher }` as follows:

        cache: new InMemoryCache({ fragmentMatcher })

5. Run your app and check that the errors have gone.


### Resources

- See [Fragment matcher](https://www.apollographql.com/docs/react/recipes/fragment-matching.html)
