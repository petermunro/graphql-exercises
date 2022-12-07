# Setting up an Apollo Client

1.  Install `create-react-app` if you haven't already done so. Use
    it to build out a new React app. Start the local server as instructed.

2.  Install the following npm packages:

        npm install @apollo/client graphql

    Documentation:

    - [github repo](https://github.com/apollographql/react-apollo)
    - [docs](https://www.apollographql.com/docs/react/quick-start.html)

### `index.js`

3.  Import `apollo-client` and instantiate it, pointing it at your local GraphQL server:

    ```javascript
    import { ApolloClient, InMemoryCache, ApolloProvider, gql } from '@apollo/client';

    const client = new ApolloClient({
      uri: 'http://localhost:4001/graphql',
      cache: new InMemoryCache(),
    });
    ```

4.  Wrap your `<App>` in an `ApolloProvider` component:

    ```javascript
    ReactDOM.render(    // for React < v18
                        // alternatively root.render(...)
      <ApolloProvider client={client}>
        <App />
      </ApolloProvider>,
      document.getElementById('root') // for React < v18
    );
    ```

### `App.js`

6.  Import the Apollo client libraries:

    ```javascript
    import { useQuery, gql } from '@apollo/client';
    ```

7.  Add your query. For example, let's make a "hello" query:

    ```javascript
    const GET_HELLO_WORLD = gql`
      query GetHelloWorld {
        system {
          hello
        }
      }
    `;
    ```


8.  Now we just need to render the data received. I recommend installing the React DevTools if you haven't already done so, to view the component's props so you can see the data returned by the server. I added a paragraph to my `App` render function as follows:

    ```js
    function App() {
      const { loading, error, data } = useQuery(GET_HELLO_WORLD);

      return (
        <div className="App">
          <header className="App-header">
            {loading && <p>Loading...</p>}
            {error && <p>An error occurred</p>}
            <p>{data?.system?.hello}</p>
          </header>
        </div>
      );
    }
    ```

### Questions for you

1.  The Apollo team has taken the approach of enabling you to simply copy
    a query from _GraphiQL_ and paste it into your code. What do you think
    of Apollo's approach?
2.  If a component has a tree of nested children, how could the GraphQL response
    data be propagated down them?

### Further Steps

Next steps to take are:

1.  Investigate `this.props.data.loading`, and implement a "Loading…" spinner.
2.  Refactor the code into a `System` component. What props might this component
    receive?
