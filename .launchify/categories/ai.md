# AI and LLM Security

**Category ID:** `ai`

---

## Scope

Inspect all AI, LLM, and machine learning integrations for prompt injection, model security, output validation, and AI-specific risks.

---

## Checks

### Prompt Injection
- Prompt injection
- Indirect prompt injection
- System prompt leakage
- Users extracting hidden instructions
- Jailbreaks
- Missing jailbreak resistance

### Output Safety
- Unsafe AI output
- Missing output validation
- AI-generated HTML executed unsafely
- AI-generated code executed unsafely
- AI-generated commands executed unsafely
- Hallucination-driven security failures
- Fake permissions, fake approvals, incorrect actions

### Permissions and Control
- Excessive AI permissions
- Agent overreach
- Unrestricted tools
- Sensitive actions without approval
- Missing approval boundaries
- AI-generated code execution
- Unsafe command execution
- Missing sandboxing

### Data Protection
- Sensitive data sent to models
- Sensitive data in prompts
- Prompt data retention leaks
- Sensitive prompts stored indefinitely

### Model Security
- Model endpoint exposure
- Public OpenAI-compatible model endpoints without authentication
- Public local-model endpoints without authentication
- Unauthenticated model APIs
- Model abuse
- Training data leakage
- Model inversion
- Model extraction

### Supply Chain
- AI supply-chain risk
- Model supply-chain risk
- Downloaded models with malware or backdoors
- Unverified model files
- Unsafe model plugins
- Untrusted tools
- Tool-output injection
- Context-window manipulation

### Controls
- Missing prompt and output logging controls
- Excessive prompt retention
- Missing tenant isolation in model context
- Cross-user context leakage
- Missing model access controls
- Missing model cost controls
- Denial-of-service through expensive prompts
- Unbounded token usage
- Unbounded tool loops
- Missing model fallback safety
- Missing human approval gates
- AI performing irreversible actions automatically
- AI accessing secrets unnecessarily
- AI accessing production systems unnecessarily
- AI-generated content trusted without validation
- AI-generated policy or permission decisions without deterministic enforcement
- AI-generated security decisions without human or rule-based controls

---

## Methodology

1. Identify all AI/LLM integration points
2. Test for prompt injection on all user-facing AI inputs
3. Verify output validation is applied to AI responses
4. Check AI permission boundaries and approval gates
5. Verify sensitive data is not sent to models unnecessarily
6. Check model endpoint authentication and access controls
7. Verify tenant isolation in AI context
8. Check for AI cost controls and rate limiting
9. Verify human approval gates for irreversible actions
10. Check for AI-generated content validation

---

## Severity Guide

| Finding | Typical Severity |
|---|---|
| Prompt injection allowing code execution | CRITICAL |
| System prompt leakage exposing security controls | HIGH |
| AI performing irreversible actions without approval | HIGH |
| Sensitive data sent to external AI provider | HIGH |
| Missing output validation on AI responses | MEDIUM |
| Unbounded token usage | MEDIUM |

---

## Evidence Requirements

- AI/LLM integration point affected
- Specific prompt or input vector
- Whether the finding is exploitable through user input
- Whether sensitive data is involved
- Impact on system integrity and data confidentiality
