# ADR 00005: Elastic for non-profit search

## Status

Proposed

## Context

Advanced search capabilities are desired to facilitate candidates finding the non-profits, facilitate candidate-with-non-profit matching as well as non-profit-with-non-profit-matching.
 
## Decision

On top of the relational database system (RDBMS) described in ADR0006 (note: not written), ElasticSearch has been selected as the denormalized data store to power the searches. All data in the relational datastore, as well as full texts from the uploaded PDFs will be ingested into Elasticsearch and available for searching. 

## Consequence

Having ElasticSearch power the non-profit searches, gives:
- Low response latency - due to search-optimized, denormalized and distributed nature of the solution, low latency is expected
- Elastic's [query DSL](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl.html) offers language construct for exact matches (in search scenarios's) as well as queries with 'match scores' - more suitable for discovery.
- PDF full-text (describing the non-profit service offerings) can easily be stored in elastic and be included in search results. 

### Rejected Tradeoff:
- Direct querying of the RDBMS. Joining large datasets for searching is typically an expensive operation in SQL. Also, full-text search cabilities are limited and less performant.

#### Benefits lost due to rejecting tradeoff:
- Cost impact: search-optimized datastore can imply additional cost
- Solution complexity: development, deployment and monitoring complexity
- Security impact: additional attack vector because more solution components
- Team competence: additional technology that needs to be used by the team