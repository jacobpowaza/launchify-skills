# AI Agent Security

**Category ID:** `agents`

---

## Scope

Inspect all AI agent configurations, tool permissions, autonomy levels, and agent-specific security controls. AI agents have superuser access by default — without guardrails, a compromised agent can destroy your entire system.

---

## Checks

### Permissions and Tools
- Excessive agent permissions (agent has more access than needed)
- Unnecessary tools (agent has tools it doesn't use)
- Unrestricted filesystem access (agent can read/write any file)
- Unrestricted database access (agent can query/modify any table)
- Unrestricted browser access (agent can browse any URL)
- Unrestricted network access (agent can connect to any service)
- Destructive actions without approval (delete, drop, overwrite, truncate)
- Sending messages without approval where inappropriate (email, Slack, SMS)
- Unsafe code execution (agent can run arbitrary code)
- Missing sandboxing (agent runs in same context as application)
- Missing tool permission boundaries
- Agent can send emails without approval
- Agent can delete files without approval
- Agent can access databases without approval
- Agent can execute code without approval
- Agent can modify infrastructure without approval
- Agent can deploy to production without approval
- Agent can change permissions without approval
- Agent can access unrelated tenants
- Agent can access secrets without approval
- Agent can bypass approval workflows
- Agent can approve its own actions

### Injection and Manipulation
- Tool-output injection (attacker-controlled data in tool results affects agent behavior)
- Agent memory poisoning (malicious content stored in agent memory affects future actions)
- Unsafe autonomy (agent makes decisions without human oversight)
- Untrusted content passed directly to privileged tools
- Prompt injection targeting agent (user input influencing agent tool calls)
- Indirect prompt injection through external data sources
- Context manipulation through conversation history
- Agent confused by adversarial inputs

### Control and Governance
- Missing action auditing (no log of what agent did)
- Missing rollback or recovery capability
- Confused-deputy vulnerabilities (agent authorized, acts on behalf of unauthorized user)
- Credential exposure to tools (agent has access to credentials it shouldn't)
- Missing action allowlists and denylists
- Missing rate limits and tool-call limits
- Missing loop limits (agent runs indefinitely)
- Missing cost limits (agent uses unlimited tokens)
- Missing transaction boundaries (agent performs partial operations)
- Missing dry-run mode (agent always makes real changes)
- Missing human approval gates
- Missing reversible operations (agent performs irreversible actions)
- Missing action confirmation (agent acts without confirming intent)
- Missing agent identity (agent actions not attributed to specific agent)
- Missing agent audit trail (no history of agent actions)
- Missing agent session isolation (agents share state)
- Missing memory isolation (agent memory accessible to other agents)
- Missing prompt and tool provenance (no tracking of where prompts/tools came from)
- Missing recovery after partial failure

### Browser and External Communication
- Unsafe browser automation (agent navigates to untrusted URLs)
- Unsafe external communication (agent sends data to untrusted services)
- Unsafe file or command execution (agent runs untrusted files)
- Agent browsing untrusted websites
- Agent downloading untrusted files
- Agent executing downloaded code
- Agent communicating with attacker-controlled servers

### Deployment and Infrastructure
- Agent able to deploy to production
- Agent able to modify infrastructure-as-code
- Agent able to modify CI/CD pipelines
- Agent able to modify access controls
- Agent able to modify monitoring/alerting
- Agent able to modify logging configuration
- Agent able to access production databases
- Agent able to modify production data

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
11. Test tool-output injection
12. Test agent memory poisoning
13. Verify agent cannot approve its own actions
14. Check agent cannot access unrelated tenants

---

## Severity Guide

| Finding | Typical Severity |
|---|---|
| Agent can execute arbitrary code without approval | CRITICAL |
| Agent can access production databases | CRITICAL |
| Agent can deploy to production without approval | HIGH |
| Agent can approve its own actions | HIGH |
| Agent memory poisoning through untrusted input | HIGH |
| Tool-output injection affecting agent behavior | HIGH |
| Missing action audit trail | MEDIUM |
| Missing cost limits | MEDIUM |
| Missing loop limits | MEDIUM |

---

## Evidence Requirements

- Agent technology and configuration
- Specific tool or permission affected
- Whether the agent has access to production systems
- Whether approval gates are enforced
- Impact on system integrity and data confidentiality
- Whether the agent can modify its own approval gates
