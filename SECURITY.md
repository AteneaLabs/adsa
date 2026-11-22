# ADSA Security Boundary

ADSA is a research prototype that **generates and executes Python code**. Its current repair path may also ask a model to introduce package-install commands when dependencies are missing.

## Treat generated code as untrusted

Do not run ADSA directly on a workstation/server that contains production credentials, valuable files or unrestricted infrastructure access.

Recommended minimum controls:

1. Run in a disposable container or VM.
2. Mount only the files required for the experiment.
3. Use least-privilege, revocable API credentials.
4. Keep production/cloud credentials out of the runtime.
5. Restrict outbound network access when the experiment does not require it.
6. Do not supply sensitive/private datasets unless the execution environment and model-provider data policy are explicitly appropriate.
7. Review generated `solution.py` before using it outside an isolated research environment.
8. Treat dynamically proposed package installation as untrusted software supply-chain input.

## Current non-guarantees

The repository does not currently provide a hardened sandbox, package allowlist, syscall isolation, filesystem capability model, egress firewall, signed dependency policy or production multi-tenant security boundary.

Timeouts limit execution duration; they are **not** a security sandbox.

## Secrets

`.env` is ignored by Git. Never commit real Azure OpenAI or Anthropic API keys. If a credential is accidentally published, revoke/rotate it rather than relying on Git history cleanup alone.

## Reporting

For security findings, contact Atenea Labs through the current contact channel published by the organization/repository owner. Do not include active credentials, private datasets or exploit payloads containing third-party sensitive data in public issues.
