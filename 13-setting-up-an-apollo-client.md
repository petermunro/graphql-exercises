# Setting up an Apollo Client

1. Install `create-react-app` if you haven't already done so. Use it to build out a new React app. Start the local server as instructed.

2. Install the following npm packages:

        npm install apollo-client apollo-cache-inmemory apollo-link-http react-apollo graphql-tag graphql ---save

    Documentation:

    - [github repo](https://github.com/apollographql/react-apollo)
    - [docs](https://www.apollographql.com/docs/react/quick-start.html)

### `index.js`

3. Import `apollo-client` and instantiate it, pointing it at your local GraphQL server:

        import { ApolloClient } from 'apollo-client';
        import { HttpLink } from 'apollo-link-http';
        import { InMemoryCache } from 'apollo-cache-inmemory';

        const client = new ApolloClient({
          link: new HttpLink(),
          cache: new InMemoryCache(),
        });


4. Import `ApolloProvider`:

        import { ApolloProvider } from 'react-apollo';

5. Create an `ApolloProvider` component, which will wrap components in your React tree:

        ReactDOM.render(
          <ApolloProvider client={client}>
            <App />
          </ApolloProvider>,
          document.getElementById('root')
        );

### `App.js`

6. Import the Apollo client libraries:

        import { graphql } from 'react-apollo';
        import gql from 'graphql-tag';

7. At the bottom of the file, after the `App` component class, remove the `export default App;` clause. We will set up the GraphQL query and wrap the `App` component using the `graphql()` function to make the retrieved data available to our `App` component:

        const MyQuery = gql`query MyQuery {
          system {
            hubname
            uptime
          }
        }`;

        const MyAppWithData = graphql(MyQuery)(App);
        export default MyAppWithData;

8. Now we just need to render the data received. I recommend installing the [React devtools](https://github.com/facebook/react-devtools) if you haven't already done so, to view the component's props so you can see the data returned by the server. I added a paragraph to my `App` render function as follows:

        class App extends Component {
          render() {
            let system = this.props.data.system;
            return (
              ...
              <p>
                  Uptime: <span>{system && system.uptime} </span>
              </p>
              ...

### Questions for you

1. The Apollo team has taken the approach of enabling you to simply copy a query from _GraphiQL_ and paste it into your code. What do you think of Apollo's approach?
2. If a component has a tree of nested children, how could the GraphQL response data be propagated down them?

### Further Steps

Next steps to take are:

1. Investigate `this.props.data.loading`, and implement a "Loading…" spinner.
2. Refactor the code into a `System` component. What props might this component receive?
