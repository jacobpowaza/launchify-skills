# AI Agent Security

**Category ID:** `agents`

---

## Scope

Inspect all AI agent configurations, tool permissions, autonomy levels, and agent-specific security controls.

---

## Checks

### Permissions and Tools
- Excessive agent permissions
- Unnecessary tools
- Unrestricted filesystem access
- Unrestricted database access
- Unrestricted browser access
- Destructive actions without approval
- Sending messages without approval where inappropriate
- Unsafe code execution
- Missing sandboxing
- Missing tool permission boundaries

### Injection and Manipulation
- Tool-output injection
- Agent memory poisoning
- Unsafe autonomy
- Untrusted content passed directly to privileged tools

### Control and Governance
- Missing action auditing
- Missing rollback or recovery capability
- Confused-deputy vulnerabilities
- Credential exposure to tools
- Agents able to send emails, delete files, access databases
- Agents able to execute code, modify infrastructure
- Agents able to deploy to production
- Agents able to change permissions
- Agents able to access unrelated tenants
- Agents able to access secrets
- Agents able to bypass approval workflows
- Agents able to approve their own actions
- Missing action allowlists and denylists
- Missing rate limits and tool-call limits
- Missing loop limits and cost limits
- Missing transaction boundaries
- Missing dry-run mode
- Missing human approval gates
- Missing reversible operations
- Missing action confirmation
- Missing agent identity
- Missing agent audit trail
- Missing agent session isolation
- Missing memory isolation
- Missing prompt and tool provenance
- Missing recovery after partial failure

### Browser and External Communication
- Unsafe browser automation
- Unsafe external communication
- Unsafe file or command execution

---

## Methodology

1. Enumerate all agents and their available tools
2. Map tool permissions to agent responsibilities
3. Identify credentials available to each agent
4. Check for approval gates on privileged actions
5. Test whether untrusted text can influence tool execution
6. Verify actions are reversible and audited
7. Check agent session and memory isolation
8. Verify agent identity and audit trail
9. Check for human approval gates on irreversible actions
10. Verify cost and rate limits are configured

---

## Severity Guide

| Finding | Typical Severity |
|---|---|
| Agent can execute arbitrary code without approval | CRITICAL |
| Agent can access production databases | CRITICAL |
| Agent can deploy to production without approval | HIGH |
| Agent memory poisoning through untrusted input | HIGH |
| Missing action audit trail | MEDIUM |
| Missing cost limits | MEDIUM |

---

## Evidence Requirements

- Agent technology and configuration
- Specific tool or permission affected
- Whether the agent has access to production systems
- Whether approval gates are enforced
- Impact on system integrity and data confidentiality
