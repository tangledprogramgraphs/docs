---
sidebar_position: 1
---

# Linux Installation

## Quick Start

This code is designed to be used in Linux. If you use Windows, you can use Windows Subsystem for Linux (WSL). You can work with WSL in Visual Studio Code by following [this tutorial](https://code.visualstudio.com/docs/remote/wsl-tutorial). Run this to automatically install all dependencies and compile:

```bash
bash ./setup.sh
```

This performs the setup and compilation of the steps below. If you want to manually install, follow the instructions below.

For MacOS or Windows users, you can follow this [guide](dev-container.md) to setup Dev Containers which spins up a Linux based environment right within VS Code.

### 1. Install required software

From the [framework](https://github.com/tangledprogramgraphs/framework) directory run:

```
sudo xargs --arg-file requirements.txt apt install
```

Note that [MuJoco](https://mujoco.org/) must be downloaded and unpacked separately.

### 2. Set environment variables

In order to easily access tpg scripts, we add appropriate folders to the $PATH environment variable.
To do so, add the following to _~/.profile_

```
export TPG=<YOUR_PATH_HERE>/tpg
export PATH=$PATH:$TPG/scripts/plot
export PATH=$PATH:$TPG/scripts/run
export MUJOCO=<YOUR_PATH_TO_MUJOCO>/mujoco-3.2.2
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$MUJOCO/lib/
```

Then run:

```
source ~/.profile
```

### 3. Compile

From the tpg directory run:

```bash
cmake -B build -S . -DCMAKE_BUILD_TYPE=Release
cmake --build build --config Release
```

To run in debug mode:

```bash
cmake -B build -S . -DCMAKE_BUILD_TYPE=Debug
cmake --build build
```

To run the build with compiler optimization flags:

```bash
cmake -B build -S . -DCMAKE_BUILD_TYPE=Release -DENABLE_HIGH_OPTIMIZATION=ON
cmake --build build
```

Additionally, you can use the `Makefile` to build TPG as well.

To build in debug mode:

```bash
make debug
```

To build in release mode:

```bash
make release
```

To build with optimized flags:

```bash
make optimized
```

To clean the Build:

```bash
make clean
```
