# .claude/agents

Agent definitions for the jesus-songs project. Each `.md` file is a self-contained agent: frontmatter declares the model and tools; the body is the agent's prompt.

See [AGENTS.md](AGENTS.md) for the registry, pipelines, and output locations.

## Adding a new agent

1. Copy the format of an existing agent file.
2. Set `name`, `description`, `model`, and `tools` in frontmatter.
3. Write the agent body — input contract, process, rubric/format, rules.
4. Add a row in `AGENTS.md`.
5. If the agent should be invokable as a slash command, add a file under `../commands/`.

## Running

Use `/review-songs` from the parent Claude Code session. The orchestrator reads `AGENTS.md`, spawns agents per the pipeline, and writes results under `.claude/agent-output/`.
