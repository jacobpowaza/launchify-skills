# RAG and Vector Security

**Category ID:** `rag`

---

## Scope

Inspect all Retrieval-Augmented Generation (RAG) pipelines, vector databases, embedding systems, and document retrieval security. RAG systems expose internal documents to AI — without proper access control, anyone can query your entire knowledge base.

---

## Checks

### Vector Database Security
- Exposed vector databases (no authentication required)
- Missing vector database authentication
- Embedding or vector database leaks (cross-tenant data)
- Vector database accessible from public internet
- Missing vector database backups and recovery
- Missing vector database monitoring
- Missing ingestion audit logs
- Vector database credentials hardcoded
- Vector database without encryption at rest
- Vector database without encryption in transit
- Vector database without access logging

### Retrieval Authorization
- RAG authorization bypass (user retrieves documents they shouldn't see)
- Unauthorized document retrieval
- Missing document-level ACLs
- Cross-tenant retrieval (user A retrieves user B's documents)
- Metadata-filter bypass (bypassing tenant filters)
- Missing source authorization checks
- Retrieval results trusted without access validation
- Deleted documents remaining retrievable from vector index
- Stale permissions in embeddings (permissions changed, embeddings not updated)
- Missing row-level security on vector database
- Missing column-level security on vector database
- Vector search bypassing application authorization
- Missing authorization on embedding API
- Missing authorization on vector database admin endpoints
- Document access control not propagated to vector index

### Data Poisoning
- Vector poisoning (malicious documents inserted into knowledge base)
- Malicious documents inserted through user uploads
- Malicious documents inserted through third-party integrations
- Unsafe embeddings (embeddings containing malicious content)
- Sensitive information indexed accidentally
- Embedding model poisoning
- Missing content validation before indexing
- Missing document sanitization before embedding
- Adversarial documents crafted to influence retrieval

### Injection Through Content
- Document-based prompt injection (malicious instructions in indexed documents)
- Prompt injection through emails processed by RAG
- Prompt injection through PDFs processed by RAG
- Prompt injection through websites processed by RAG
- Prompt injection through documents processed by RAG
- Malicious links in retrieved content
- Prompt injection through OCR text in images
- Prompt injection through code snippets in documents
- Prompt injection through database content in RAG

### Data Management
- Missing tenant-aware indexing
- Missing deletion propagation (document deleted but embedding remains)
- Sensitive metadata leakage in vector search results
- Embedding inversion risks (extracting source text from embeddings)
- Unrestricted vector search (no query limits)
- Unbounded retrieval (returning too many results)
- Retrieval denial-of-service (expensive similarity searches)
- Missing document provenance (no tracking of where documents came from)
- Missing ingestion validation
- Unsafe HTML ingestion
- Unsafe PDF ingestion
- Unsafe email ingestion
- Unsafe website ingestion
- Missing document deduplication
- Missing document versioning
- Missing embedding update when source document changes

---

## Methodology

1. Identify all vector databases and RAG pipelines
2. Verify vector database authentication and access controls
3. Test retrieval authorization for cross-tenant access
4. Check document-level ACL enforcement
5. Test for metadata-filter bypass
6. Verify deleted documents are removed from index
7. Check for sensitive information in embeddings
8. Test ingestion pipelines for malicious content
9. Verify prompt injection through retrieved content
10. Check tenant-aware indexing and isolation
11. Verify deletion propagation works
12. Check vector database network restrictions
13. Test for unauthorized access to vector database admin

---

## Severity Guide

| Finding | Typical Severity |
|---|---|
| Cross-tenant retrieval of sensitive documents | CRITICAL |
| Prompt injection through retrieved documents | HIGH |
| Exposed vector database without authentication | HIGH |
| Sensitive information indexed in embeddings | HIGH |
| Deleted documents remaining retrievable | MEDIUM |
| Unbounded retrieval causing denial-of-service | MEDIUM |
| Missing document-level ACLs | HIGH |
| Vector poisoning | HIGH |

---

## Evidence Requirements

- Vector database technology and configuration
- RAG pipeline architecture
- Whether tenant isolation is enforced
- Whether document-level ACLs are enforced
- Data sensitivity of indexed content
- Whether deletion propagation works
- Whether content is sanitized before indexing
