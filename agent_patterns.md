# Agent Orchestration Patterns

<br>
<br>

```mermaid
---
title: Basic Chat
---
graph LR
    A(( user )) --> B{ LLM } --> C(( user ))
```

<br>
<br>
<br>

```mermaid
---
title: Basic RAG
---
flowchart LR
    A(( user )) --> B{ LLM } --> C[ API call] --> D{ LLM } --> E(( user ))
```

<br>
<br>
<br>

```mermaid
---
title: Iterative RAG
---
flowchart LR
    A(( user )) --> B{ LLM } --> C@{shape: processes, label: " API calls " } --> D{ LLM }--> E(( user ))
    C --> B
```

<br>
<br>
<br>

```mermaid
---
title: Clarify the Question
---
flowchart LR
    A(( user )) --> B{ LLM } --> C@{ shape: braces, label: "nested process" } --> E(( user ))
    B --> A
```
Often, users don't write descriptive prompts, and as a result they get very generic responses. To address this problem, this pattern imitates the human behavior of asking clarifying questions before attempting to answer the question. The LLM can be told to do so via the system prompt.

<br>
<br>
<br>

```mermaid
---
title: Plan and Execute
---
flowchart LR
    A((user)) --> B{LLM}
    X{LLM}
    B --> C@{ shape: braces, label: "nested process" } --> X
    B --> D@{ shape: braces, label: "nested process" } --> X
    B --> E@{ shape: braces, label: "nested process" } --> X
    X --> Y((user))
```
Often, LLMs can generate better responses if they are instructed to create a plan for how to answer a question, instead of attempting to answer it directly. Subprocesses are then spawned to solve parts of the plan. This narrower focus allows each subprocess to generate a richer answer.

<br>
<br>

```mermaid
---
title: Multiple Personas
---
flowchart LR
    A(( user )) --> B{ Persona 1 } --> C{ Persona 2 } --> D(( user ))
    C --> B
```
For use cases that require creative problem solving, it can be useful to have an LLM with two or more "personas" have a conversation with itself. This can be achieved with a different system prompt creating each persona.