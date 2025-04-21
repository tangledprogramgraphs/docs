---
sidebar_position: 5
---

# Future Work

This page outlines the planned improvements and future directions for the Tangled Program Graphs framework. We welcome contributions and feedback on these initiatives.

## System Architecture and Infrastructure

### Microservices Orchestration

The framework is being restructured into a service-oriented architecture with clear separation of concerns. The current architecture looks like this:

![Current Architecture: API wraps CLI commands, which then wrap mpirun commands to execute C++ binaries compiled from the engine](/img/current-arch.png)

This architecture represents a significant migration from the current implementation where the API wraps CLI commands. The new design:

- Eliminates the CLI dependency in the API service
- Enables direct interaction with C++ binaries
- Improves performance by removing unnecessary process spawning
- Reduces complexity in the API service implementation

The planned architecture reorganizes these components into:

![Planned Architecture: Framework repository contains engine, binaries, and API service. CLI communicates via network requests](/img/planned-arch.png)

- **[Framework Repository](https://github.com/TangledProgramGraphs/framework):** Contains the C++ engine code, build system, and API service. This unified repository produces both the C++ binaries and the API service that directly interfaces with them.
- **[CLI Repository](https://github.com/TangledProgramGraphs/cli):** A Python-based command-line interface distributed as a pip package. The CLI communicates with the API service via HTTP requests (e.g., `tpg evolve <env>` triggers a POST to `your-service-url/evolve`).
  For guidance on CLI code organization, refer to [authed-identity CLI](https://github.com/authed-dev/authed-identity/tree/main/authed/cli) which demonstrates a clean separation of:

  - `commands/` - Individual command implementations
  - `utils/` - Shared utilities and helpers
  - Core CLI setup and configuration files

- **API Service:** Acts as an intermediary service that supports multiple execution modes:
  - **Live-Streaming Mode:** Used by web clients (e.g., Playground) to receive real-time updates via WebSocket connections
  - **Non Live-Streaming Mode:** Used by the CLI for batch processing and non-interactive tasks
  - **Business Logic**:
    - Routes requests to the appropriate build mode based on the client type
    - Executes C++ binaries on the server
    - Manages WebSocket connections for live-streaming clients
    - Returns results to clients

This architecture decouples the CLI from the engine's execution environment, enabling:

- Independent distribution of the CLI package
- Remote execution of computationally intensive tasks
- Scalable deployment of the API service
- Clear separation of concerns between components
- Flexible execution modes for different client types

Key implementation challenges include:

- Managing service dependencies and versioning
- Ensuring reliable communication between components
- Implementing robust error handling and monitoring
- Maintaining security across service boundaries
- Coordinating different build modes and their respective client interactions
- Migrating existing API endpoints from CLI command wrapping to direct binary interaction

### Digital Research Alliance (DRA) Experiment Integration

We plan to integrate a comprehensive system for managing and analyzing DRA experiments within [TPG Playground](https://github.com/TangledProgramGraphs/playground). This will involve:

- **Automated Experiment Data Upload:** Implementing automated data upload to a centralized database after each DRA experiment is completed (either automatically or manually triggered via the CLI).
- **Experiment Database:** Developing a robust database schema to store experiment metadata, results, configurations, and environment seeds.
- **Interactive Experiment Analysis:** Creating an interface that allows researchers to:
  - View experiment results, replay simulations by seed and environment, and generate relevant plots.
  - Search and filter experiments based on various criteria.
  - Compare experiment performance and configurations.

This DRA integration is a substantial engineering undertaking that will greatly enhance the reproducibility, analysis, and sharing of research results.

## Performance Optimization

### GPU Acceleration

Continued research and investigation into leveraging GPUs to significantly improve framework performance, focusing on:

- **Parallel Evaluation:** Implementing GPU-accelerated parallel evaluation of TPG agents to optimize evolution time.
- **Memory Management:** Optimizing memory transfer and management between CPU and GPU.

## Algorithm Improvements and Multi-Task Learning

### Multi-Task Learning Enhancements

- **Novel GP Approaches:** Investigating alternative genetic programming approaches to boost the diversity, specialization, and competition of components within MTRL-TPG.
- **Selection and Mutation Improvements:** Enhance selection and mutation strategies to make the algorithms smarter in determining convergence rate.

## Get Involved

We welcome contributions from the community! If you're interested in working on any of these areas or have suggestions for additional improvements, please:

1. Check our [GitHub repository](https://github.com/tangledprogramgraphs)
2. Review our contribution guidelines
3. Join our community discussions
4. Submit pull requests with your improvements

This roadmap is continuously evolving, and we welcome feedback and suggestions from our user community.
