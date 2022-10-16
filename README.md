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

## Configuration

- Store all configurable variables/parameters in config files. Try to avoid using in-line literals/primitives. This will make it easier to find and maintain all configurable parameters when they are in one place.
- Never store sensitive configuration variables (passwords/API keys/secret keys etc) in plain text in a configuration files or source code.
- Store sensitive configuration variables, or variables that change depending on environment, as [environment variables](https://en.wikipedia.org/wiki/Environment_variable) ([dotenv](https://www.npmjs.com/package/dotenv) is a nice package for that) or as a [Docker/Kubernetes secrets](https://www.bogotobogo.com/DevOps/Docker/Docker_Kubernetes_Secrets.php).
- Create hierarchical config files that are grouped into sections. If possible, create multiple files for different configs (like database config, API config, tasks config etc).
- Application should fail and provide the immediate feedback if the required environment variables are not present at start-up. [env-var](https://www.npmjs.com/package/env-var) is a nice package for nodejs that can take care of that.
- For most projects plain object configs may be enough, but there are other options, for example: [NestJS Configuration](https://docs.nestjs.com/techniques/configuration), [rc](https://www.npmjs.com/package/rc), [nconf](https://www.npmjs.com/package/nconf) or any other package.

Example files:

- [database.config.ts](https://github.com/inobrega/aws-lambda-nestjs-boilerplate/blob/main/src/configs/database.config.ts) - database config that uses environmental variables and also validates them
- [.env.example](https://github.com/inobrega/aws-lambda-nestjs-boilerplate/blob/main/.env.example) - this is [dotenv](https://www.npmjs.com/package/dotenv) example file. This file should only store dummy example secret keys, never store actual development/production secrets in it. This file later is renamed to `.env` and populated with real keys for every environment (local, dev or prod). Don't forget to add `.env` to [.gitignore](https://github.com/inobrega/aws-lambda-nestjs-boilerplate/blob/main/.gitignore) file to avoid pushing it to repo and leaking all keys.
