# RAG and Vector Security

**Category ID:** `rag`

---

## Scope

Inspect all Retrieval-Augmented Generation (RAG) pipelines, vector databases, embedding systems, and document retrieval security.

---

## Checks

### Vector Database Security
- Exposed vector databases
- Missing vector database authentication
- Embedding or vector database leaks
- Missing vector database backups and recovery
- Missing vector database monitoring
- Missing ingestion audit logs

### Retrieval Authorization
- RAG authorization bypass
- Unauthorized document retrieval
- Missing document-level ACLs
- Cross-tenant retrieval
- Metadata-filter bypass
- Missing source authorization checks
- Retrieval results trusted without access validation
- Deleted documents remaining retrievable
- Stale permissions in embeddings

### Data Poisoning
- Vector poisoning
- Malicious documents inserted into the knowledge base
- Unsafe embeddings
- Sensitive information indexed accidentally

### Injection Through Content
- Document-based prompt injection
- Prompt injection through emails, PDFs, websites, documents
- Malicious links in retrieved content

### Data Management
- Missing tenant-aware indexing
- Missing deletion propagation
- Sensitive metadata leakage
- Embedding inversion risks
- Unrestricted vector search
- Unbounded retrieval
- Retrieval denial-of-service
- Missing document provenance
- Missing ingestion validation
- Unsafe HTML, PDF, email, or website ingestion

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

---

## Evidence Requirements

- Vector database technology and configuration
- RAG pipeline architecture
- Whether tenant isolation is enforced
- Whether document-level ACLs are enforced
- Data sensitivity of indexed content
