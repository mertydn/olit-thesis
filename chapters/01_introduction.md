# Chapter 1: Introduction

## 1.1 The Computational Dilemma in Modern Bioinformatics

High-throughput technologies—such as next-generation sequencing, single-cell transcriptomics, and mass spectrometry-based proteomics—have turned biological research into a heavily data-driven field. Today, a single study can easily generate gigabytes of raw genomic reads. Extracting meaningful biological insights from these datasets requires complex analytical pipelines, involving steps like quality control, reference alignment, statistical normalization, and variant calling.

To make high-performance computing more accessible, the bioinformatics community has widely adopted workflow management platforms. **Galaxy** is a leading example: an open-source, web-based platform designed for reproducible and transparent analysis. It allows researchers to run thousands of command-line tools without needing to manage Unix systems, compile packages, or handle software containers. Through its visual workflow canvas and built-in metadata tracking, Galaxy automatically records the provenance of every dataset.

However, despite its user-friendly interface and a repository of over 10,000 tools, a significant learning curve remains. Biologists without computational backgrounds still face several practical hurdles:

1. **Tool Selection:** There are often multiple tools available for the exact same task (e.g., aligners like Bowtie2, BWA-MEM, and HISAT2). Each has different input requirements, algorithmic assumptions, and performance trade-offs, making it difficult to choose the right one.
2. **Parameter Complexity:** Bioinformatics software typically exposes dozens of sensitive parameters, such as mismatch penalties or statistical thresholds. Choosing inappropriate settings can silently bias or invalidate downstream results.
3. **Workflow Assembly and Troubleshooting:** Linking different analytical steps together requires a solid grasp of data formats (e.g., FASTQ, BAM, VCF) and file transformations. When a tool fails, diagnosing the underlying issue is often difficult without command-line experience.

As a result, researchers often have to rely heavily on specialized bioinformatics core facilities, which can slow down the pace of discovery.

## 1.2 Autonomous AI Agents

Alongside developments in bioinformatics, the development of Large Language Models has introduced new possibilities for automating computational tasks. Modern LLMs can interpret complex instructions, maintain contextual information, and generate code for a range of technical applications beyond generating text. An important development in this area is the emergence of autonomous software agents, which extend the capabilities of LLMs by enabling them to decompose user requests into individual tasks, interact with external tools, and modify their execution strategies in response to errors.

The application of such agents in science is already being explored in several domains. ChemCrow, for example, integrates language models with chemistry-related tools, while GeneGPT enables interaction with biological databases through domain-specific APIs. These systems demonstrate how LLMs can serve as interfaces between natural-language instructions and existing scientific software, reducing the need for users to interact directly with individual tools and their underlying interfaces.

Despite these developments, deploying AI agents within established bioinformatics platforms introduces several technical challenges:

- **Hallucinations and Invalid Parameters:** LLMs may generate references to non-existent tools, unsupported command-line arguments, or invalid dataset identifiers. These errors can lead to failed workflow executions without mechanisms to validate generated commands against the available software environment.
- **Provenance and Reproducibility:** Scientific workflows require transparent execution records to ensure that results can be inspected and reproduced. When AI agents execute arbitrary scripts outside the platform's workflow management system, important information about commands, parameters, intermediate results, and execution history may not be captured.
- **Infrastructure and Security Risks:** Integrating AI agents into multi-user scientific platforms also raises deployment and access-control concerns. Depending on their architecture, agents may require additional backend services, isolated execution environments, or access to command-line tools.

## 1.3 The Galaxy AI Ecosystem: Orbit and Orbit Lite

The Galaxy Project initiated the development of native AI assistance environments to address these challenges. Two complementary architectural paradigms have emerged within this ecosystem:

1. **Orbit (Galaxy Core Agent):** Orbit represents the comprehensive, system-level AI environment for Galaxy. It operates within the core infrastructure as a standalone service, providing an AI agent with access to the operating system and shell. Orbit is optimized for those requiring arbitrary package installations, and deep system automation.
2. **Orbit Lite (Olit):** In contrast to Orbit's system-level runtime, **Olit** is developed as a lightweight, zero-installation, browser-resident AI co-scientist. Olit lives directly inside the client's web browser. It executes within a standard Galaxy visualization plugin without requiring administrative privileges.

Throughout this thesis, Orbit Lite is referred to as **Olit**. Olit operates through standardized Galaxy REST APIs and an isolated, in-browser WebAssembly Python environment (Pyodide). This architectural divergence represents a trade-off: Olit trades raw shell access for universal accessibility, zero server cost, client-side credential security, and total integration with Galaxy.

## 1.4 Problem Statement and Research Objectives

This thesis argues that an autonomous AI agent can be built to run entirely within a user's web browser to manage complex bioinformatics workflows.

Driven by this premise, the primary research question is:

> *"How reliably can a browser-native AI agent prepare and visualize scientific data using Galaxy, and what practical limitations and architectural improvements emerge from a systematic evaluation?"*

To answer this research question, the study is structured across three core investigative phases. First, we explore the client-side Web Worker runtime and in-browser Python execution, examining how the agent can inherit the user's existing session authentication and interact directly with the Galaxy REST API without requiring dedicated backend containers. Second, we evaluate how effectively the agent maps complex dataset columns to declarative visualization schemas (`galaxy-charts`), systematically identifying canonical failure modes and formulating automated self-correction routines. Finally, we assess the agent's ability to use local Python execution to clean malformed tabular data and calculate basic scientific metrics directly in the browser, avoiding the clutter of trivial data-wrangling jobs in the user's main Galaxy history.

To operationalize these phases, the research pursues four concrete technical objectives:

- **O1. Runtime Design:** The system must maintain conversational memory across page reloads and operate strictly without requiring dedicated backend compute containers.
- **O2. User-Controlled Execution:** Implement a *Plan First, Run Second* protocol to keep the human in the loop. This ensures that the agent cannot execute workflows or perform actions without user approval, keeping all parameter choices fully transparent.
- **O3. On-Demand Skill Retrieval:** Create a modular *Skills* system that feeds the agent verified technical instructions only when needed. This approach prevents hallucinations, while also securing the system against prompt injection.
- **O4. Provenance and Documentation:** Develop a pipeline that automatically tracks the analytical process. It should seamlessly convert executed Galaxy jobs, parameter settings, and interactive charts into permanent, shareable Galaxy Page notebooks.

## 1.5 Summary of Contributions

The primary contributions described in this thesis are as follows:

- **Olit Architectural Framework:** We present the design of Olit, the first browser-native AI co-scientist for Galaxy, demonstrating that multi-turn workflow planning and execution can be realized within client-side Web Workers.
- **Comparative Architectural Analysis:** We articulate the distinct operational boundaries between system-level agents (Orbit) and platform-bound agents (Olit), demonstrating how Olit's architectural boundaries intentionally expose missing features in Galaxy core.
- **Dynamic Skills Knowledge System:** We implement an on-demand skills routing and vendoring mechanism that delivers verified procedural guidance for notebook generation and visual analytics without context-window degradation.
- **Interactive Visual Analytics and Notebook Synthesis:** We integrate the Galaxy Charts framework with client-side Vega-Lite compilation, enabling both temporary exploratory charting and permanent durable visualization objects embedded within reproducible Galaxy Page reports.

## 1.6 Thesis Organization

The remainder of this thesis is structured as follows:

- **[Chapter 2 (Background and Related Work)](./02_background.md):** Reviews the Galaxy computational model, the evolution of autonomous AI agents in science, the technical foundations of client-side browser computing and related scientific agent platforms.
- **[Chapter 3 (System Design and Methodology)](./03_architecture.md):** Details the architecture of Olit, including UI-worker decoupling, the Skills router, visual analytics integration and session resumability.
- **Chapter 4 (Hands-on Case Study and Walkthrough):** Documents a complete experimental demonstration across sequential phases, analyzing intermediate artifacts, interactive parameter adjustments and final scientific report generation.
