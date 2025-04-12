---
sidebar_position: 5
---

# Future Work

This page outlines the planned improvements and future directions for the Tangled Program Graphs framework. We welcome contributions and feedback on these initiatives.

## System Architecture and Infrastructure

### Microservices Orchestration

A significant engineering effort is planned to migrate the framework towards a microservices architecture. This involves decoupling components like the API, CLI, C++ Framework core, and Web Application (Playground) into independently deployable services. Key challenges include:

- **Dependency Management:** Orchestrating dependencies between the services, especially given the CLI's dependency on the C++ binaries and the API's reliance on the CLI.
- **Scalability and Resilience:** Designing a scalable and resilient architecture capable of handling increasing user load and complex experiment workflows.
- **Communication Protocols:** Implementing efficient and reliable communication protocols between the microservices.
- **Deployment and Monitoring:** Establishing automated deployment pipelines and comprehensive monitoring tools.

### Distributed Research Automation (DRA) Experiment Integration

We plan to integrate a comprehensive system for managing and analyzing DRA experiments. This will involve:

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

- **Parallel Evaluation:** Implementing GPU-accelerated parallel evaluation of TPG agents to reduce training time.
- **Kernel Optimization:** Developing optimized GPU kernels for key TPG operations.
- **Memory Management:** Optimizing memory transfer and management between CPU and GPU.

## Algorithm Improvements and Multi-Task Learning

### Multi-Task Learning Enhancements

- **Novel GP Approaches:** Investigating alternative genetic programming approaches to boost the diversity, specialization, and competition of components within MTRL-TPG.
- **Selection and Mutation Improvements:** Enhance selection and mutation strategies to make the algorithms smarter in determining convergence rate.

### Core Framework

- Optimization of parallel execution in MPI implementation
- Enhanced memory management for large-scale experiments
- Improved logging and debugging capabilities
- Extended support for custom environment configurations

### MuJoCo Integration

- Support for additional MuJoCo environments
- Enhanced visualization capabilities for policy debugging
- Real-time policy visualization improvements
- Integration with newer MuJoCo versions as they become available

## Developer Tools

### Playground Web Application

- Enhanced real-time experiment monitoring
- Interactive policy visualization tools
- Improved experiment comparison interface
- Extended debugging capabilities

### CLI Improvements

- Additional automation scripts for common workflows
- Enhanced experiment management features
- Improved data export capabilities
- Better integration with external analysis tools

## Documentation and Community

### Documentation

- Expanded tutorials and examples
- More comprehensive API documentation
- Additional guides for common use cases
- Better troubleshooting guides

### Community Support

- Enhanced contribution guidelines
- Community showcase section
- Regular release notes and updates
- Improved issue templates and documentation

## Get Involved

We welcome contributions from the community! If you're interested in working on any of these areas or have suggestions for additional improvements, please:

1. Check our [GitHub repository](https://github.com/tangledprogramgraphs)
2. Review our contribution guidelines
3. Join our community discussions
4. Submit pull requests with your improvements

This roadmap is continuously evolving, and we welcome feedback and suggestions from our user community.
