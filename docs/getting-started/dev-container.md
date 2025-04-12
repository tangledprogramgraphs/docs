---
sidebar_position: 2
---

# Dev Containers Installation

This guide will help you get started with the TPG developer environment using Dev Containers which spins up a reproducible environment for those who aren't on Linux

## Prerequisites

Before you begin, make sure you have the following installed on your system:

1. Docker
2. VS Code
3. Dev Containers VS Code Extension

## Setting up Docker

1. Download and install Docker for your operating system:

   - [Docker Desktop for Windows](https://docs.docker.com/docker-for-windows/install/)
   - [Docker Desktop for Mac](https://docs.docker.com/docker-for-mac/install/)

2. Run the following command to ensure Docker is running properly

```
docker --version
```

## Activating the Dev Container in VS Code

1. Open [framework](https://github.com/tangledprogramgraphs/framework) on Visual Studio Code.

2. When VS Code detects the Dev Container configuration, you'll see a
   notification in the bottom-right corner. Click on "Reopen in Container" to
   start the Dev Container.

Alternatively, you can:

- Press `CMD + SHIFT + P` on Mac or `CTRL + SHIFT + P` on Windows to open the command palette
- Type `Dev Containers: Reopen in Container` and select it

3. VS Code will now build and start the Dev Container. This may take a few
   minutes the first time.

4. Once the Dev Container is ready, you'll see the VS Code window reload, and
   you'll be working inside the container environment.

## Debugging

- If `Dockerfile` or `devcontainer.json` were modified, need to run `Dev Containers: Rebuild without Cache and Reopen in Container`.
- If you run into this error:

```shell
--------------------------------------------------------------------------
A call to mkdir was unable to create the desired directory:

  Directory: /tmp/ompi.486db9b350d8.1000/pid.9240
  Error:     No space left on device

Please check to ensure you have adequate permissions to perform
the desired operation.
--------------------------------------------------------------------------
[486db9b350d8:09240] [[48619,0],0] ORTE_ERROR_LOG: Error in file ../../../orte/util/session_dir.c at line 107
[486db9b350d8:09240] [[48619,0],0] ORTE_ERROR_LOG: Error in file ../../../orte/util/session_dir.c at line 346
--------------------------------------------------------------------------
It looks like orte_init failed for some reason; your parallel process is
likely to abort.  There are many reasons that a parallel process can
fail during orte_init; some of which are due to configuration or
environment problems.  This failure appears to be an internal failure;
here's some additional information (which may only be relevant to an
Open MPI developer):

  orte_session_dir failed
  --> Returned value Error (-1) instead of ORTE_SUCCESS
--------------------------------------------------------------------------
```

Run the `Dev Containers: Rebuild without Cache and Reopen in Container` to create a new development environment. This could become an issue if you are using the same container for a while. We will be investigating this issue further.

## Benefits of Using Dev Containers

Our Dev Container provides a consistent, pre-configured development environment
with the following advantages:

- All necessary dependencies and tools are pre-installed
- TPG code will be built, developers can start running experiments right away
- Consistent development environment across different machines and operating
  systems
- Easy onboarding for new team members
- Isolated environment that doesn't affect your local system
