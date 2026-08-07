# Phase 6 – One feature at a time

Never implement multiple features simultaneously.

# Phase 7 – Test continuously

Every module should have tests before moving on.

# Phase 8 – Never skip integration

After every module

Implement

↓

Test

↓

Integrate

↓

Commit
I would use the CLI LLM almost exclusively

For this project

Architecture:

Occasional ChatGPT

Everything else

CLI

because

it sees the repository
it can edit files
it can search
it remembers the project structure
it is much faster
I would avoid asking open-ended questions

Instead of

Implement the workflow engine.

Ask

Implement the configuration loader.

Later

Implement the Git abstraction.

Later

Implement workflow state validation.

Each prompt should correspond to roughly 1–3 hours of implementation, not days.

Use Git aggressively

Every completed task:

Task

↓

Tests

↓

Commit

Small commits.

Never large commits.

Keep the engine deterministic

Avoid LLM logic inside the engine.

The engine should never decide.

It should only

validate
parse
route
generate prompts
check prerequisites
execute configured commands
enforce transitions

The LLMs provide intelligence.

The engine provides correctness.
