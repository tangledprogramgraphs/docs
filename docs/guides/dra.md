---
sidebar_position: 1
---

# DRA Experiment Execution

The Digital Research Alliance of Canada (aka "The Alliance") provides High Performance Parallel Compute (HPPC) reseources to Canada's research community. This includes servers with many parallel CPUs, GPUs, FPGAs, and more. We primarily use many CPUs.

### Resources

[Technical Documentation](https://docs.alliancecan.ca/wiki/Technical_documentation)

### Quick Start

Pick a [compute cluster](https://docs.alliancecan.ca/wiki/National_systems#Compute_clusters) to use and login via ssh. We'll use [narval](https://docs.alliancecan.ca/wiki/Narval). Note you'll need to setup [multifactor authentication](https://docs.alliancecan.ca/wiki/Multifactor_authentication).

```
ssh [USERNAME]@narval.alliancecan.ca
```

Move to ~/projects/def-skelly and create your personal directory.

```
cd ~/projects/def-skelly
mkdir [USERNAME]
cd [USERNAME]
```

Set up your environment variables to automatically load when you login by adding the following to the end of your `~/.bash_profile` file (replace [USERNAME] with your username):

```
export TPG=$HOME/projects/def-skelly/[USERNAME]/tpg
export PATH=$PATH:$TPG/scripts/plot
export PATH=$PATH:$TPG/scripts/run
export MUJOCO=$HOME/projects/def-skelly/[USERNAME]/mujoco-3.2.2
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$MUJOCO/lib/

module load \
  StdEnv/2023 scipy-stack/2023b python/3.10 \
  arrow/15.0.1 gcc/12.3 opencv/4.9.0 cmake/3.27.7 \
  eigen/3.4.0 boost-mpi/1.82.0 glfw/3.3.8 tbb/2021.10.0 \
  hdf5/1.14.2

```

Note that you will need to install [mujoco](https://mujoco.org/) as specified in your `.bash_profile`.

After editing `.bash_profile`, run:

```
source ~/.bash_profile
```

Clone this repo and cd to its root directory:

```
git clone https://gitlab.cas.mcmaster.ca/kellys32/tpg.git
cd tpg
```

`tpg/scripts/run/tpg-run-slurm.sh` is a generalized [job script](https://docs.alliancecan.ca/wiki/Running_jobs). Each experiment folder may also have a specialized script. These job scripts set parameters such as how many nodes and cpus you need and which [time limit queue](https://docs.alliancecan.ca/wiki/Job_scheduling_policies#Time_limits) you want to place your job in. In general, shorter jobs that use less resources will run sooner. See [scheduling policies](https://docs.alliancecan.ca/wiki/Job_scheduling_policies) for complete details.

In our example, each job (experiment repeat) will use 64 cpus and we want them all on the same node, so we use an entire 64-cpu node. The default time limit is 3 hours. Our `tpg-run-slurm.sh` job script looks like this:

```
#!/bin/bash
#SBATCH --account=def-skelly
# single node
#SBATCH --nodes=1
#SBATCH --ntasks-per-node=64
#SBATCH --mem=0
#SBATCH --time=0-3:00  # time (DD-HH:MM)

#defaults
mode=0 #Train:0, Replay:1, Debug:2
seed=1
while getopts m:s: flag
do
   case "${flag}" in
      m) mode=${OPTARG};;
      s) seed=${OPTARG};;
   esac
done
if [ $mode -eq 0 ]; then
  srun ../build/release/cpp/experiments/TPGExperimentMPI -s $seed \
  1> tpg.$seed.$$.std 2> tpg.$seed.$$.err
fi
```

For each unique experiment, best practice is to copy the experiment directory and append a unique date, time, and git revision like this:

```
cp -r mujoco/ mujoco-reacher-`date +%Y-%m-%d-%H-%M-%S`-`git rev-parse --short HEAD`
```

From inside the newly created experiment directory, we run serveral experiments at once using unique seeds. Here's an example command using a for loop:

```
for seed in `seq 1 3`; do sbatch $TPG/scripts/run/tpg-run-slurm.sh -s $seed -p $TPG/configs/<yaml_file>; done
```

To [monitor](https://docs.alliancecan.ca/wiki/Running_jobs#Monitoring_jobs) your job use:

```
squeue -u [USERNAME]
```

To cancel a job:

```
scancel <jobid>
```

To cancel all your running jobs:

```
scancel -u [USERNAME]
```

**Copying data from clusters to you local computer**

You can use `scp` to copy data from the cluster to you local computer. Here's an example command to run locally:

```
scp -r skelly@narval.alliancecan.ca:/home/skelly/projects/def-skelly/skelly/tpg/experiment_directories/mujoco-reacher-2024-11-27-07-57-05-b997160 ./
```

The `-r` flag indicates you want to copy the directory and all its contents recursively.

Note that you can also transfer data using other ssh clients such as [FileZilla](https://filezilla-project.org/) or [WinSCP](https://docs.alliancecan.ca/wiki/Multifactor_authentication#WinSCP).
