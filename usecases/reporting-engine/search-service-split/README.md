# Externalized Search Service

## 🧠 Context
Text search inside a transactional DB is slow and limited. Moving to a specialized engine like Elasticsearch or MeiliSearch boosts performance and flexibility.

## 🎯 Goal
Split search into its own service:
- Uses optimized indexing engine
- Handles full-text, fuzzy, and relevance-based queries
- Syncs data via event-driven updates

## 🛠 Architecture Sketch
- Main app emits `EntityUpdated` and `EntityDeleted` events
- SearchIndexer service syncs data to index
- Search API handles user queries with filters, ranks, etc.

## ✅ Implementation Tips
- Use Elasticsearch or MeiliSearch with SDK
- Add index versioning and sync tracking
- Include reindexing CLI for full refresh
