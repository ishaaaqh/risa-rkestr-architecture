# Search Architecture

## MVP

PostgreSQL-backed search.

PostgreSQL remains authoritative.

## Capabilities

- Free text
- Structured filters
- Sorting
- Cursor pagination
- Saved views
- Productivity views
- Authorization-aware queries
- Bulk operations

## Authorization

Search must enforce authorization inside the query boundary.

The UI must never retrieve unauthorized data and hide it afterward.

## Pagination

Cursor-based pagination is the default for high-volume interactive lists.

Sorting must be deterministic using a stable secondary key.

## Future OpenSearch

OpenSearch is an extraction option when scale or search requirements justify it, such as:
- fuzzy search
- typo tolerance
- relevance ranking
- very large datasets
- advanced text search

The Search module should keep an abstraction seam for future replacement.
