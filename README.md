# Olit: A Browser-Native Autonomous AI Co-Scientist for the Galaxy Bioinformatics Platform

**Master's Thesis Draft**  
**Author:** Ali Mert Aydın  
**Institution:** Universität Freiburg / Bioinformatics  
**Date:** November 2026

---

## Abstract

Galaxy is widely used to analyze large volumes of biological data. Despite the wide range of tools available through its community, using these resources can be challenging for biologists without a computational background. Combining tools into multi-step workflows, selecting appropriate parameters and resolving errors often requires experience with bioinformatics and programming. Large Language Models (LLMs) offer a possible way to make these tasks more accessible. However, many existing AI agents operate on remote servers and rely on system-level access, such as root privileges and shell environments. This raises practical concerns about computational costs, container management, and the handling of sensitive data.

Within the Galaxy ecosystem, Orbit was developed as an AI co-scientist that operates as a server-side agent. Unlike Orbit, this thesis presents Olit, an AI co-scientist that runs entirely within the user's web browser and integrates directly into the Galaxy web interface. By operating client-side, Olit makes use of the user's existing Galaxy session without requiring dedicated server infrastructure, keeping API credentials and execution locally in the browser.

Olit is designed to keep users involved in the analysis process. It follows a Plan First, Run Second approach: before any jobs are submitted to Galaxy, the agent proposes a workflow and its associated parameters, which the user can review and approve. An on-demand Skills Router provides the agent with relevant technical knowledge when required, rather than loading all available information into the context window at once. Olit also integrates with Galaxy Charts to support interactive data visualization and can generate shareable Galaxy Pages that document the analysis and its results.

The thesis describes Olit's architecture and implementation, examines the trade-offs between browser-based and server-side AI agents, and evaluates the system through a case study involving biological data exploration.

---

## Table of Contents

1. **[Chapter 1: Introduction](./chapters/01_introduction.md)**
   - [1.1 The Computational Dilemma in Modern Bioinformatics](./chapters/01_introduction.md#11-the-computational-dilemma-in-modern-bioinformatics)
   - [1.2 Autonomous AI Agents](./chapters/01_introduction.md#12-autonomous-ai-agents)
   - [1.3 The Galaxy AI Ecosystem: Orbit and Orbit Lite](./chapters/01_introduction.md#13-the-galaxy-ai-ecosystem-orbit-and-orbit-lite)
   - [1.4 Problem Statement and Research Objectives](./chapters/01_introduction.md#14-problem-statement-and-research-objectives)
   - [1.5 Summary of Contributions](./chapters/01_introduction.md#15-summary-of-contributions)
   - [1.6 Thesis Organization](./chapters/01_introduction.md#16-thesis-organization)
2. **[Chapter 2: Background and Related Work](./chapters/02_background.md)**
   - [2.1 The Galaxy Scientific Computing Model](./chapters/02_background.md#21-the-galaxy-scientific-computing-model)
   - [2.2 LLMs and Autonomous Agents in Bioinformatics](./chapters/02_background.md#22-llms-and-autonomous-agents-in-bioinformatics)
   - [2.3 Where Does the Agent Live?](./chapters/02_background.md#23-where-does-the-agent-live)
   - [2.4 System-Level vs. Platform-Bound AI Architectures: Orbit vs. Olit](./chapters/02_background.md#24-system-level-vs-platform-bound-ai-architectures-orbit-vs-olit)
   - [2.5 Browser-Side Computing](./chapters/02_background.md#25-browser-side-computing)
   - [2.6 Security, Safety, and Privacy in Scientific AI](./chapters/02_background.md#26-security-safety-and-privacy-in-scientific-ai)
3. **[Chapter 3: System Design and Methodology](./chapters/03_architecture.md)**
   - [3.1 System Architectural Overview](./chapters/03_architecture.md#31-system-architectural-overview)
   - [3.2 Human-in-the-Loop](./chapters/03_architecture.md#32-human-in-the-loop)
   - [3.3 The Dynamic Skills Knowledge Architecture](./chapters/03_architecture.md#33-the-dynamic-skills-knowledge-architecture)
   - [3.4 Data Visualization and Interactive Analytics](./chapters/03_architecture.md#34-data-visualization-and-interactive-analytics)
   - [3.5 Session Resumability and Automated Notebooks](./chapters/03_architecture.md#35-session-resumability-and-automated-notebooks)
4. **[Bibliography](#bibliography)**

---

## Bibliography

1. **Bran, A. M., Cox, S., Schilter, O., Baldassari, C., White, A. D., & Schwaller, P.** (2023). ChemCrow: Augmenting large-language models with chemistry tools. *arXiv preprint arXiv:2304.05376*.
2. **Di Tommaso, P., Chatzou, M., Floden, E. W., Barja, P. P., Palumbo, E., & Notredame, C.** (2017). Nextflow enables reproducible computational analysis. *Nature Biotechnology*, 35(4), 316–319.
3. **Droettboom, M., et al.** (2018). Pyodide: Bringing the Python scientific stack to the browser. In *SciPy Conference*.
4. **Goecks, J., Nekrutenko, A., & Taylor, J.** (2010). Galaxy: a comprehensive approach for supporting accessible, reproducible, and transparent computational research in the life sciences. *Genome Biology*, 11(8), R86.
5. **Haas, A., Rossberg, A., Schuff, D. L., Titzer, B. L., Holman, M., Gohman, D., Wagner, L., Zakai, A., & Bastien, J. F.** (2017). Bringing the web up to speed with WebAssembly. *ACM SIGPLAN Notices*, 52(6), 185–200.
6. **Jin, Q., Yang, Y., Chen, Q., & Lu, Z.** (2024). GeneGPT: Augmenting large language models with domain tools for improved access to biomedical information. *Bioinformatics*, 40(2), btae075.
