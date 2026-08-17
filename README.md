# Generative AI process records for a medical ethics commentary

[![DOI](https://img.shields.io/badge/DOI-10.5281%2Fzenodo.21959480-007ec6)](https://doi.org/10.5281/zenodo.21959480)

This repository documents how generative AI was used in preparing the manuscript *Available upon reasonable request: the authorship function that was already dead*, intended for submission to [*JME Practical Bioethics*](https://jmepb.bmj.com/).

The purpose of this repository is transparency. It gives readers a clearer view of which AI tools were used, what they were asked to do, and how their outputs contributed to the manuscript. It is written for readers with or without a technical background.

## Process at a glance

```mermaid
%%{init: {
  "flowchart": {
    "htmlLabels": true,
    "curve": "basis",
    "nodeSpacing": 48,
    "rankSpacing": 52,
    "padding": 32,
    "wrappingWidth": 300
  },
  "themeVariables": {
    "fontSize": "16px"
  }
}}%%
flowchart TD
    classDef human fill:#eff6ff,stroke:#1d4ed8,stroke-width:2px,color:#1e3a8a,rx:8px,ry:8px;
    classDef aiPrimary fill:#faf5ff,stroke:#7e22ce,stroke-width:2px,color:#3b0764,rx:8px,ry:8px;
    classDef aiSub fill:#ffffff,stroke:#9333ea,stroke-width:1.5px,stroke-dasharray:4 4,color:#581c87,rx:8px,ry:8px;
    classDef aiEdit fill:#f0fdf4,stroke:#15803d,stroke-width:2px,color:#14532d,rx:8px,ry:8px;

    H1["👤 <b>Human Direction & Ideation</b><br/>Conceives core arguments & sets task scope"]:::human

    subgraph S1 ["<b> Phase 1: Research & Drafting (Harness: Claude Cowork) </b>"]
        direction TB
        B1["💡 <b>Fable 5 (Brainstorming)</b><br/>Interacts with human to surface blindspots & refine scope"]:::aiPrimary

        F1["🚀 <b>Fable 5 (Task Coordinator)</b><br/>Implements plans & dispatches subagents"]:::aiPrimary

        O1["🤖 <b>Opus 5 Subagent</b><br/>Literature search"]:::aiSub
        O2["🤖 <b>Opus 5 Subagent</b><br/>Fact verification"]:::aiSub
        O3["🤖 <b>Opus 5 Subagent</b><br/>Novelty scanning"]:::aiSub

        F2["📝 <b>Fable 5 (Synthesis)</b><br/>Compiles subagent outputs into raw draft"]:::aiPrimary
    end

    H2["👤 <b> Human Review & Steering</b><br/>Evaluates raw draft & plans agent setup and pipeline for editing"]:::human

    subgraph S2 ["<b> Phase 2: Editing (Harness: Claude Code CLI) </b>"]
        direction TB
        E1["⚙️ <b>Claude Code CLI + CLIProxyAPI </b>"]:::aiEdit
        E2["✨ <b>Gemini 3.1 Pro</b><br/>Structural and language editing"]:::aiEdit
    end

    H3["👤 <b> Human Verification & Revision</b><br/>Manually audits references, revises text & takes full responsibility"]:::human

    H1 --> B1
    B1 --> F1
    F1 --> O1
    F1 --> O2
    F1 --> O3
    O1 --> F2
    O2 --> F2
    O3 --> F2
    F2 --> H2
    H2 --> E1
    E1 --> E2
    E2 --> H3
  ```

In simple terms, the author supplied the ideas, source material, and direction. AI tools helped search and organize the literature, check specific facts, draft an early version, and improve its structure and language. The author then reviewed and revised the work and remains responsible for the manuscript.

## Repository contents

| File | What it contains |
| --- | --- |
| [`Claude_Cowork_process_record.yaml`](Claude_Cowork_process_record.yaml) | A concise record of the Claude-assisted literature search, fact-checking, novelty scan, synthesis, and initial drafting.|
| [`Claude_Code_CLI_process_record.yaml`](Claude_Code_CLI_process_record.yaml) | A record of the structural and language editing performed by Gemini 3.1 Pro. It records the versions of Claude Code CLI, [CLIProxyAPI](https://github.com/router-for-me/CLIProxyAPI), and [george-orwell-skill](https://github.com/Emberwhirl/george-orwell-skill) versions used for the session. The original editing prompt is preserved. |

YAML is a plain-text format for structured information. The two YAML files can be read directly in a web browser or text editor. No specialist software is required.

## Tools and recorded versions

The tables below record the models, agent environments, and supporting tools used in preparing the manuscript. Versions are those used at the time, where known; they are not necessarily the latest available versions.

### AI models

| Name | Version or identifier |
| --- | --- |
| Claude Fable 5 | `claude-fable-5` |
| Claude Opus 5 | `claude-opus-5` |
| Gemini 3.1 Pro | `gemini-3.1-pro-preview` |

### Agent environments and harnesses

| Name | Version |
| --- | --- |
| Claude Code CLI | `2.1.233` |
| Claude Cowork | Unavailable (online service) |

### Supporting tools and skills

| Name | Version |
| --- | --- |
| [CLIProxyAPI](https://github.com/router-for-me/CLIProxyAPI) | `7.2.86` |
| [george-orwell-skill](https://github.com/Emberwhirl/george-orwell-skill) | `0.1.0` |

These details improve the interpretability of the process records, but they do not create a fully reproducible software environment. In particular, managed services may change without exposing a platform version, and model outputs remain stochastic.

## Human responsibility

The AI systems are not listed as authors. The human author developed the central arguments, selected the material used in the manuscript, evaluated and revised AI-generated text, checked the correctness and relevance of the cited references, and manually worked with the reference management software when preparing the manuscript. The human author approved the manuscript and accepts responsibility for its content.

These records do not replace editorial review, peer review, or independent verification of the manuscript's claims.

## Limitations

- The records were reconstructed retrospectively by the AI systems from their available session context; they are not provider-generated audit logs.
- The first phase used Claude Cowork as a managed online service. Its exact platform version was not available for this retrospective record.
- Agent tasks are stochastic: the same systems and instructions may produce different outputs on another run. These records therefore promote transparency and accountability but do not ensure reproducibility in the strict sense.
- A process record shows how a tool was used. It does not by itself establish that every AI output was correct or that a literature search was exhaustive.

## Acknowledgments

The author gratefully acknowledges the following open-source projects, public posts, and discussions that informed the technical setup and/or writing workflow:

- [@trq212's guide to prompting Claude Fable 5](https://x.com/trq212/article/2073100352921215386), which informed the prompting approach for better working with Claude Fable 5.
- [忒修斯的船板 (@Arcadia_Bao)](https://x.com/Arcadia_Bao) and [宝玉 (@dotey)](https://x.com/dotey), whose posts and discussions offered useful perspectives on AI-assisted writing. 宝玉's work is also available on [GitHub](https://github.com/JimLiu).
- [Vox (@Voxyz_ai)](https://x.com/Voxyz_ai) for posts connecting George Orwell's writing principles with AI-assisted writing. The cited posts are available [here](https://x.com/Voxyz_ai/status/2078857041087545737) and [here](https://x.com/Voxyz_ai/status/2079136199524950526).
- The open-source agent skill [george-orwell-skill](https://github.com/Emberwhirl/george-orwell-skill), used as a writing-style instruction.
- The [CLIProxyAPI](https://github.com/router-for-me/CLIProxyAPI) project, which provided the compatibility bridge used in the later editing phase.
- [Theo – t3.gg (@theo)](https://x.com/theo) and [Tibo (@thsottiaux)](https://x.com/thsottiaux) for their public discussion and instructions on running models through Claude Code with CLIProxyAPI, informally called "Claudex". Their relevant posts are available [here (Theo)](https://x.com/theo/status/2076114415368482854) and [here (Tibo)](https://x.com/thsottiaux/status/2076119366647894371). This inspired the related "**Claudemini**" setup used for this project.

## License

Copyright © 2026 Yu-Tian Xiao.

Unless otherwise stated, the README, Mermaid diagram, and YAML process records in this repository are licensed under the [Creative Commons Attribution-NonCommercial 4.0 International License](https://creativecommons.org/licenses/by-nc/4.0/). The complete legal text is provided in the [`LICENSE`](LICENSE) file.

Linked third-party materials and projects remain subject to their respective licences. The manuscript is not covered by this repository licence unless expressly stated otherwise.

## Archiving and citation

Version `v1.0.0` is permanently archived on [Zenodo](https://zenodo.org/records/21959480).

**Recommended citation:**

> Xiao, Yu-Tian. (2026). *JMEPB_GenAI_authorship_commentary* (v1.0.0) [Workflow]. Zenodo. [https://doi.org/10.5281/zenodo.21959480](https://doi.org/10.5281/zenodo.21959480)
