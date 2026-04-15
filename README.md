# SkillGraph Runtime

**Contract-based procedural skills for LLM agents.**

Turn static `SKILL.md`-style artifacts into executable, composable, and testable skill modules with typed inputs/outputs, preconditions, postconditions, and DAG-based execution.

## What is SkillGraph Runtime?

Traditional agent skills are usually stored as static prompt artifacts, such as `SKILL.md`, templates, and supporting files. They are useful, but hard to validate, compose, reuse, and maintain as systems grow.

SkillGraph Runtime upgrades skills from **document-style knowledge artifacts** into **contract-based procedural modules**.

With SkillGraph Runtime, a skill is no longer just a prompt. It becomes a structured unit with:

- typed inputs and outputs
- explicit preconditions and postconditions
- parameter binding
- DAG-based composition
- executable runtime semantics
- built-in validation and tests

This makes skills easier to reuse across tasks, safer to execute, and much easier to debug, benchmark, and evolve.

## Why this project?

Current agent ecosystems are strong at:

- calling tools
- chaining prompts
- loading reusable skill documents

But they are still missing a clean abstraction between **prompt artifacts** and **executable procedural capabilities**.

SkillGraph Runtime fills this gap by introducing a lightweight skill specification, a compiler to Skill IR, and a runtime that executes skills as composable graph modules.

## Core ideas

SkillGraph Runtime is built around four ideas:

1. **Skill Contract**  
   Every skill declares typed inputs/outputs, constraints, and execution metadata.

2. **Skill IR**  
   Skills are compiled into a normalized intermediate representation for analysis, validation, and execution.

3. **Skill DAG**  
   A skill can be composed from multiple steps or subskills connected as a directed acyclic graph.

4. **Skill Validation**  
   Every skill can ship with executable test cases and post-execution assertions.

## From static skills to procedural modules

```text
skill.yaml + prompts + tests
            │
            ▼
        Skill Compiler
            │
            ▼
          Skill IR
            │
            ▼
       SkillGraph Runtime
            │
            ├─ validate contracts
            ├─ execute DAG
            ├─ call subskills/tools
            └─ generate traces
```

## Features

- Define skills with a structured `skill.yaml`
- Typed inputs and outputs
- Explicit preconditions and postconditions
- Compile skills into a normalized Skill IR
- Execute skills as DAGs
- Support LLM nodes, Python nodes, Tool nodes, and Subskill nodes
- Built-in skill testing and output assertions
- Execution traces for debugging and observability

## Repository structure

```text
skillgraph-runtime/
├─ README.md
├─ LICENSE
├─ pyproject.toml
├─ .gitignore
├─ docs/
│  ├─ spec.md
│  ├─ ir.md
│  ├─ runtime.md
│  ├─ testing.md
│  └─ examples.md
├─ src/
│  └─ skillgraph_runtime/
│     ├─ __init__.py
│     ├─ spec/
│     │  ├─ models.py
│     │  ├─ parser.py
│     │  └─ validator.py
│     ├─ compiler/
│     │  ├─ ir.py
│     │  ├─ compile.py
│     │  └─ dag_check.py
│     ├─ runtime/
│     │  ├─ executor.py
│     │  ├─ context.py
│     │  ├─ state.py
│     │  ├─ trace.py
│     │  └─ nodes/
│     │     ├─ base.py
│     │     ├─ llm_node.py
│     │     ├─ python_node.py
│     │     ├─ tool_node.py
│     │     └─ subskill_node.py
│     ├─ contracts/
│     │  ├─ preconditions.py
│     │  ├─ postconditions.py
│     │  └─ matchers.py
│     ├─ testing/
│     │  ├─ runner.py
│     │  └─ reporters.py
│     ├─ cli/
│     │  └─ main.py
│     └─ adapters/
│        ├─ llm_base.py
│        ├─ openai_adapter.py
│        └─ mock_adapter.py
├─ skills/
│  ├─ summarize-paper/
│  │  ├─ skill.yaml
│  │  ├─ README.md
│  │  ├─ prompts/
│  │  │  ├─ plan.md
│  │  │  └─ summarize.md
│  │  └─ tests/
│  │     └─ basic.yaml
│  ├─ extract-entities/
│  │  ├─ skill.yaml
│  │  ├─ prompts/
│  │  └─ tests/
│  └─ write-email/
│     ├─ skill.yaml
│     ├─ prompts/
│     └─ tests/
├─ tests/
│  ├─ unit/
│  ├─ integration/
│  └─ fixtures/
└─ examples/
   ├─ inputs/
   └─ outputs/
```

## Roadmap

- [ ] v0.1 Skill spec
- [ ] v0.1 Compiler -> Skill IR
- [ ] v0.1 Runtime executor
- [ ] v0.1 Test runner
- [ ] v0.2 Subskills and parameter binding
- [ ] v0.2 Trace visualization

## Vision

SkillGraph Runtime aims to bridge the gap between reusable skill documents and executable agent capabilities.

The long-term goal is to make skills:

- **typed** enough to validate
- **composable** enough to build systems
- **testable** enough to trust
- **observable** enough to debug
- **modular** enough to evolve

## License

MIT
