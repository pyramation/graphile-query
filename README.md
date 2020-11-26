# graphile-query

```sh
npm install graphile-query
```

## usage

Use as a particular role, skipping any auth logic

```js
const results = await client.query({
    role: 'postgres',
    query,
    variables
});
```

Or pass a request object to be evaluated based on logic

```js
const results = await client.query({
    req: { something: { special: 'e90829ef-1da4-448d-3e44-b3d275702b86' } },
    query: MyGraphQLQuery,
    variables
});
```

## initialization

```js
import { GraphileQuery, getSchema } from 'graphile-query';

// get the pg pool
const pool = getRootPgPool();

// get Graphile Settings
const settings = getGraphileSettings({
    schema: [SCHEMA_NAME],
    pgSettings (req) {
        // custom logic for requests
        return { role: 'public' };
    }
});

// get schema
const schema = await getSchema(pool, settings);

// initialize client
const client = new GraphileQuery({ schema, pool, settings });
```
