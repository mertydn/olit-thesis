# Chapter 2: Background and Related Work

## 2.1 The Galaxy Scientific Computing Model

Galaxy is one of the most widely used open-source workflow platforms in the life sciences, serving tens of thousands of researchers through large public servers like usegalaxy.eu [4]. The platform is built around a few core concepts designed to ensure that scientific analyses remain transparent and reproducible:

### 2.1.1 Histories, Datasets, and Provenance Graphs

In Galaxy, the main workspace for any analysis is the **History**. A history acts as an ordered, permanent record of all datasets generated during a session. Under the hood, every item in a history is managed as a *History Dataset Association* (HDA), which includes:

- A simple sequential number for the user interface (HID, e.g., `#1`, `#2`);
- A unique, permanent internal identifier (Encoded ID, e.g., `f2db41e1fa331b3e`);
- A specific file datatype (e.g., `fastq.gz`, `bam`, `tabular`, `vcf`) that determines which downstream tools can process it;
- A direct link to the job that created it, recording the exact tool version, parameters, standard output, and execution environment.

To track this information, Galaxy structures dataset provenance as a directed acyclic graph (DAG). This means that for any given file or final result, the system can easily trace its entire lineage—identifying every previous tool, parameter setting, and source file that contributed to its creation.

### 2.1.2 Tool Models and Metadata Discovery

x

### 2.1.3 The Galaxy Visualization Framework and Galaxy Charts

x

## 2.2 LLMs and Autonomous Agents in Bioinformatics

x

## 2.3 Where Does the Agent Live?

1. **Inside Galaxy:** ChatGXY (January 2026)
2. **Outside Galaxy:** Orbit (May 2026)
3. **The Browser as the Agent Host:** JupyterLite AI (May 2025), Orbit Lite (October 2026)

### 2.3.1 Browser Owns the Agent

Place agent ownership inside the user's web browser tab:

1. **2 GB of storage via the Origin Private File System**
2. **WebAssembly**
3. **Pyodide**
4. **Galaxy as the Operating System**
5. **Accessibility**

## 2.4 System-Level vs. Platform-Bound AI Architectures: Orbit vs. Olit

The central design consideration for integrating AI into Galaxy is the execution boundary of the agent runtime. Within the Galaxy ecosystem, this divide is embodied by **Orbit** and **Olit**.

**Table 2.1:** Architectural Comparison of Orbit and Olit

| Architectural Dimension | Orbit | Olit |
| :--- | :--- | :--- |
| Execution Runtime | Native Linux OS / Container | Web Browser Tab |
| Terminal / Shell Access | Bash Terminal | None |
| Python Execution | System Python / Conda Shell | In-Browser Pyodide |
| Authentication Method | Galaxy API Keys / MCP Protocol | Cookies |
| Infrastructure Cost | Dedicated Server / Container per User | Zero Server Overhead |
| Package Installation | Arbitrary | Strictly Galaxy Installed Tools |
| Failure Mode | Ad-hoc Shell Workaround | Exposes Missing Galaxy Features |

### 2.4.1 Orbit: The System-Level Linux Paradigm

x

### 2.4.2 Olit: The Platform-Bound Browser Paradigm

x

## 2.5 Browser-Side Computing

### 2.5.1 WebAssembly and Pyodide

### 2.5.2 Asynchronous Execution via Web Workers

### 2.5.3 Persistent Client-Side Storage via OPFS and SQLite

Browser memory is temporary: refreshing a page or closing a tab usually clears all active data. To support long-running analyses without risking data loss, Olit uses `pi-durable`, an embedded database engine. It saves conversation logs, job histories, and current tool states directly to the browser's **Origin Private File System** (OPFS) via SQLite. As a result, if a user happens to reload the page during a multi-hour job, the agent immediately recovers its exact state and picks up right where it left off.

## 2.6 Security, Safety, and Privacy in Scientific AI

### 2.6.1 Client-Side Credential Isolation
