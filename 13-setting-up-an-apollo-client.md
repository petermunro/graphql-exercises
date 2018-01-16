# Setting up an Apollo Client

1. Install `create-react-app` if you haven't already done so. Use it to build out a new React app. Start the local server as instructed.

2. Install the `react-apollo` npm package. (Its use is described [here](http://dev.apollodata.com/react/initialization.html).)

### index.js

3. Import `apollo-client` and instantiate it, pointing it at your local GraphQL server:

        import { ApolloClient, ApolloProvider, createNetworkInterface } from 'react-apollo';

        const client = new ApolloClient({
          networkInterface: createNetworkInterface({ uri: 'http://localhost:3002/graphql' }),
        });

4. Create an `ApolloProvider` component, which will wrap components in your React tree:

        ReactDOM.render(
          <ApolloProvider client={client}>
            <App />
          </ApolloProvider>,
          document.getElementById('root')
        );

### App.js

5. Import the Apollo client libraries:

        import { gql, graphql } from 'react-apollo';

6. At the bottom of the file, after the `App` component class, remove the `export default App;` clause. We will set up the GraphQL query and wrap the `App` component using the `graphql()` function to make the retrieved data available to our `App` component:

        const MyQuery = gql`query MyQuery {
          person(id: "12") {
            id
            firstName
            lastName
            city
            country
          }
        }`;

        const MyAppWithData = graphql(MyQuery)(App);
        export default MyAppWithData;

7. Now we just need to render the data received. I recommend installing the [React devtools](https://github.com/facebook/react-devtools) if you haven't already done so, to view the component's props so you can see the data returned by the server. I added a paragraph to my `App` render function as follows:

        class App extends Component {
          render() {
            let person = this.props.data.person;
            return (
              ...
              <p>
                  <span>{person && person.firstName} </span>
              </p>
              ...

### Questions for you

1. The Apollo team has taken the approach of enabling you to simply copy a query from _GraphiQL_ and paste it into your code. What do you think of Apollo's approach?
2. If a component has a tree of nested children, how could the GraphQL response data be propagated down them?

### Further Steps

Next steps to take are:

1. Investigate `this.props.data.loading`, and implement a "Loading…" spinner.
2. Refactor the code into a `PersonView` component. What props might this component receive?
3. Determine how to use query variables, so you don't hard code the `Person`s `id`. Add a text input or a menu so you can choose which id to fetch.
