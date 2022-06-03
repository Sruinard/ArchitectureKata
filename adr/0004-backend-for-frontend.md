# ADR 00004: Backend for frontend (BFF) design pattern with Federated GraphQL

## Status

Proposed

## Context

One of the key requirements it the ease of use of the platform. In order to improve ease of use, we wan't to be able to send the required data to the required platform (i.e. mobile vs desktop) such that we can focus on the UI/UX rather than data fetching.

## Decision

All frontend teams retrieve data from the federated application gateway. Due to the single large graph api that is exposed, this enables easy retrieval for the data that is required. The backend for frontend functionality is thus achieved by being selective about the fields you retrieve.

example mobile application:

```
{
    query: {
        non-profits: {
            name
            offerings
        }
    }
} --> {
    result: {
        non-profits: [
            {
            name: non_profit_a
            offerings: [
                resume_checker,
                housing_helper
            ]
        }]

    }
}
```

example desktop application (more space, so showing best matches):

```
{
    query {
        non-profits {
            name
            offerings {
                score
            }

        }
    }
} --> {
    result: {
        non-profits: [
            {
            name: non_profit_a
            offerings: [
                {
                    resume_checker: {
                        score: 0.88
                    }
                },
                {
                    housing_helper: {
                        score: 0.5
                    }
                },
            ]
        }]

    }
}
```

## Consequences

Leveraging the graph API enables us to modify the retrieval of data is the frontend consumer sees fit. This enables rapid development, ease-of-use, improved response times and an optimized UI/UX experience.

One of the downsides:

- There is a bigger learning curve (most people are familiar with RESTAPIs, but not with GraphQL)

Rejected: BFF for frontend through restapi
An alternative would be to create separate backend for frontends based on REST apis. However, due the nature of GraphQL this distinction is not needed, as you can query the data you require.

However, most developers are familiar with RESTful APIs. They might expect that the right APIs are "just" there and find it cumbersome to learn a new quering language.
