# Security Policy

## Supported Versions

All magitech-ai repositories are pre-1.0. Security updates are provided for
the latest `main` of each repository; there is no versioned support window
until the first 1.0 release.

---

## Reporting a Vulnerability

If you discover a security vulnerability in any magitech-ai repository, please
report it responsibly rather than opening a public issue.

- **Report privately** via GitHub Private Vulnerability Reporting on the
  affected repository (Security tab → Report a vulnerability), or open a
  private security advisory.
- **Include**:
  - A description of the vulnerability.
  - Steps to reproduce or proof-of-concept.
  - Affected repository and component.
  - Potential impact and suggested mitigations.

You will receive an acknowledgment within 48 hours, followed by updates on
triage, remediation, and public disclosure coordination.

---

## Threat Model & Local Execution Guidelines

Magitech software includes an agent runtime that executes model-driven tools
and generates code on behalf of the user. When running it, note the following
security invariants:

### 1. Command and Code Execution

Agent tools for shell execution and file system manipulation execute with the
permissions of the user running the process, by design.

- **Untrusted Repositories**: Do not run the agent against untrusted
  repositories without isolation. Running an autonomous agent against code
  containing adversarial instructions can lead to indirect prompt injection.
- **Sandboxing**: For untrusted workloads, run inside an isolated container,
  VM, or restricted user account.

### 2. Prompt Injection & Input Validation

LLM-based autonomous agents are inherently susceptible to direct and indirect
prompt injection. Malicious instructions embedded in files, commit messages,
or tool outputs can attempt to alter agent behavior. Process isolation remains
the primary defense.

### 3. API Key Hygiene

- API keys are resolved from environment variables or the host OS credential
  store.
- API keys are never persisted to session logs or committed to git.
- Never commit .env files or session storage containing sensitive credentials.
