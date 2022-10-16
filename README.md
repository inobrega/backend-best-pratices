# Backend Best Pratices

## API Versioning

API versioning is the practice of transparently managing changes to your API.

API versioning allows you to incorporate the latest changes in a new version of your API thereby still allowing users to have access to the older version of your API without breaking your users application.

If you need to create a new version of an endpoint, a simple solution would be to create new version of [DTOs](https://github.com/Sairyss/domain-driven-hexagon#DTOs) and a URL like this: `/v2/users`. Keep old version of an endpoint running for backwards compatibility until your users fully migrate to a new version.

Creating a new version of an endpoint instead of modifying an old one protects users of your API from breaking their app.

**Note**: if the only user of your API is your own frontend that can change on demand API versioning may be not worth it.

If you are using [GraphQL](https://graphql.org/), you can use a [@deprecated](https://dgraph.io/docs/graphql/schema/deprecated/) directive on a field.

For versioning packages, libraries, SDKs etc. you can use [semantic versioning](https://semver.org/).

Example files:

- [app.routes.ts](https://github.com/Sairyss/domain-driven-hexagon/blob/master/src/configs/app.routes.ts) - file that contains routes with its version.

Read more:

- [How to Version a REST API](https://www.freecodecamp.org/news/how-to-version-a-rest-api/)
