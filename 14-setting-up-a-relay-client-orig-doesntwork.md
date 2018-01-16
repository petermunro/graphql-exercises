# Setting up a Relay Client

1. You can again start with `create-react-app` to build out a new React app.

2. Install `babel-plugin-react-relay`:

        yarn add -D babel-plugin-react-relay

   or

        npm install -D babel-plugin-react-relay

3. Configure your GraphQL endpoint in `package.json` by adding a `"graphql"` property:

        {
          "dependencies": { ... },
          "graphql": {
            "request": {
              "url": "https://example.com/graphql"
            }
          }
        }

4. Run `yarn` or `npm install`.

5. Edit the file `./node_modules/react-scripts/config/webpack.config.dev.js`, find the line:

       presets: [require.resolve('babel-preset-react-app')],

   and add this line below it:

       plugins: [require.resolve('babel-plugin-react-relay')],

   Also, turn off `cacheDirectory` a few lines further down:

       cacheDirectory: false

6. Start the local server with `yarn start` or `npm start`.

7.
yarn add react-relay

8.

Relay.injectNetworkLayer(
  new Relay.DefaultNetworkLayer('http://localhost:3001/graphql')
);


class MeetRoute extends Relay.Route {
  static queries = {
    meet: () => Relay.QL`query { meet(id: $meetId) }`

  };

  static paramDefinitions = {
    meetId: { required: true },
  };

  static prepareParams = (prevParams) => {
    return {
      ...prevParams,
      meetId: prevParams.meetId
    }
  };

  static routeName = 'meet';
}

const meetRoute = new MeetRoute({meetId: 17});
