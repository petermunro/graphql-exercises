## Query Batching

At the moment, our client makes separate HTTP POST requests for each component's GraphQL query.

Apollo Client offers a `apollo-link-batch-http` package to help us here.

1. Install the package.

2. Import it into your `index.js`:

        import { BatchHttpLink } from "apollo-link-batch-http";

3. Instantiate a `new BatchHttpLink()` instead of a `new HttpLink()`.

4. Test your code.
