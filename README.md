<div align="center">
<h3 align="center">Tangled Program Graphs Documentation</h3>

  <p align="center">
    Documentation for the Tangled Program Graphs framework
    <br />
     <a href="https://tangledprogramgraphs.github.io/docs/">tangledprogramgraphs.github.io/docs/</a>
  </p>
</div>

## Table of Contents

<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#about-the-project">About The Project</a>
      <ul>
        <li><a href="#key-features">Key Features</a></li>
      </ul>
    </li>
    <li><a href="#built-with">Built With</a></li>
    <li><a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#prerequisites">Prerequisites</a></li>
        <li><a href="#installation">Installation</a></li>
      </ul>
    </li>
    <li><a href="#acknowledgments">Acknowledgments</a></li>
  </ol>
</details>

## About The Project

This repository contains the documentation website for the Tangled Program Graphs (TPG) framework. TPG is an open-source reinforcement learning (RL) framework built upon a genetic programming approach. The documentation is built using Docusaurus, a modern static website generator. It provides guides, API references, and tutorials to help users understand and utilize the TPG framework effectively. The documentation covers the framework's architecture, usage, and future development plans.

### Key Features

- **Comprehensive Documentation:** Provides detailed information about the TPG framework, including its architecture, components, and usage.
- **Docusaurus-Powered:** Built using Docusaurus, ensuring a modern, performant, and easily maintainable website.
- **Guides and Tutorials:** Offers step-by-step guides and tutorials to help users get started with the framework and understand its various features.
- **API Reference:** Includes a comprehensive API reference for the TPG framework, allowing developers to easily integrate it into their projects.
- **Future Work Roadmap:** Outlines planned improvements and future directions for the TPG framework, providing insights into its ongoing development.
- **CLI Documentation:** Documents the CLI tool that exposes core framework functionalities, enabling batch processing, scripting, and integration with other systems.
- **DRA Experiment Execution Guide:** Provides a guide on executing experiments on the Digital Research Alliance of Canada (DRA) infrastructure.

## Built With

- [Docusaurus](https://docusaurus.io/) - A modern static website generator
- [React](https://reactjs.org/) - A JavaScript library for building user interfaces
- [Node.js](https://nodejs.org/) - JavaScript runtime environment
- [Yarn](https://yarnpkg.com/) - Package manager
- [TypeScript](https://www.typescriptlang.org/) - A superset of JavaScript that adds static typing

## Getting Started

To get the documentation website running locally, follow these steps:

### Prerequisites

- [Node.js](https://nodejs.org/) (>=18.0)
- [npm](https://www.npmjs.com/)
- [Yarn](https://yarnpkg.com/)

### Installation

1. Clone the repository:
2. Install dependencies:

   ```sh
   npm install
   ```

3. Start the local development server:

   ```sh
   npm start
   ```

   This command starts a local development server and opens up a browser window. Most changes are reflected live without having to restart the server.

4. Deployment:

   The documentation is automatically deployed through our GitHub Actions pipeline. Any commits pushed to the `main` branch will trigger a build and deployment to the `gh-pages` branch, making the changes live on the website.

## Acknowledgments

- This README was created using [gitreadme.dev](https://gitreadme.dev) — an AI tool that looks at your entire codebase to instantly generate high-quality README files.
