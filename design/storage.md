# Storage

Much of the information is static, so the storage design will rely heavily on caching.

The bulk of the raw information (politician info, voting records, etc.) will be stored
in a SQL database. This doesn't change. The cache will be used to store computed
information, like a particular politicians' generalized stance on an issue. These
will change infrequently, so we can heavily use caching to reduce computation.

## SQL
The usual candidates for SQL servers are:
- MySQL/MariaDB: fast, but doesn't fully respect SQL spec. Unsure if it matters.
- PostgreSQL: slower than MySQL, but has better concurrency and consistency.

SQLite isn't an option, since this won't be a single reader-writer situation. There
will be lots of ongoing computations, so we need locks.

I'm leaning towards PostgreSQL because, as noted, we'll be relying on cache for most
of our reads (by user request volume).

## Caching
My first thought was Redis (since its really great at this sort of thing). But Varnish
seems like a better move, since it will automatically handle things once configured.
Redis might be useful for other things (storing intermediate results of computations,
or other cached data), but Varnish should handle the bulk, since everything is going
over HTTP.
