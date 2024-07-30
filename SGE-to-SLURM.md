
<div id="top"></div>

<!-- PROJECT SHIELDS -->
<!--
*** I'm using markdown "reference style" links for readability.
*** Reference links are enclosed in brackets [ ] instead of parentheses ( ).
*** See the bottom of this document for the declaration of the reference variables
*** for contributors-url, forks-url, etc. This is an optional, concise syntax you may use.

[![Contributors][contributors-shield]][contributors-url]
[![Forks][forks-shield]][forks-url]
[![Stargazers][stars-shield]][stars-url]
[![Issues][issues-shield]][issues-url]



<!-- PROJECT LOGO -->

<div align="center">
  <a href="https://github.com/universityofsussex-its/RC-Workshops">
    <img src="./images/logo.png" alt="Logo" width="80" height="80">
  </a>

  <h3 align="center">SGE to SLURM CHEAT SHEET</h3>
    <a href="https://github.com/universityofsussex-its/RC-Workshops"><strong>Go Back to Splash »</strong></a>
    <br />
</div>

In general every command in SGE has mirror in slurm.


### Apollo2 
On Apollo2 we used a schedular based on the Son of Grid Engine (SGE), which is the open source community version that previously continued development of Sun Grid Engine (also referred to as SGE). It's this version (Son of Grid Engine) that has been used inside of ParallelCluster. Moving off SGE to SLURM needs some adjustments in how to interact with the scheduler by using SLURM commands and adjust the submission scripts.

#### Nomenclature
* **queue/partition** SGE uses the term queues, while SLRUM calls them partitions
* **node-count** SGE has no concept of node counts, SLURM has

#### Commands
Firstly, common commands used in SGE have an equivalent in the SLURM environment. The following table reviews the most common once.
| User Command | SGE | SLURM |
|--------------|-----|---------|
| Interactive Login | `qlogin` | `srun --pty [-p $partition_name] [--time=hh:mm:ss] bash` |
| Job submission | `qsub $script_file` | `sbatch $script_file` |
| Job deletion | `qdel $job_id` | `scancel $job_id` |
| Job status by job | `qstat -u \* -j $job_id` | `squeue $job_id` |
| Job status by user | `qstat -u $user_name` | `squeue -u $user_name` |
| Job hold | `qhold $job_id` | `scontrol hold $job_id` |
| Job release | `qrls $job_id` | `scontrol release $job_id` |
| Queue list | `qconf -sql` | `squeue` |
| List nodes | `qhost	` | `sinfo -N` OR `scontrol show nodes` |
| Cluster status | `qhost -q` | `sinfo` |
| GUI | `qmon` | `sview` |
#### Environment Variables
Environment variables are used within a script to get access to information about the running job.
| Information | SGE | SLURM |
|--------------|-----|---------|
| Job ID | `$JOB_ID` | `$SLURM_JOBID` |
| Submit directory | `$SGE_O_WORKDIR` | `$SLURM_SUBMIT_DIR` |
| Submit host | `$SGE_O_HOST` | `$SLURM_SUBMIT_HOST` |
| Node list | `$PE_HOSTFILE` | `$SLURM_JOB_NODELIST` |
| Job Array Index | `$SGE_TASK_ID` | `$SLURM_ARRAY_TASK_ID` |
#### Job Specification
Submission scripts are able to inform the scheduler about certain parameters of the submission using a directive and options. The following table collects the most common specifications.
| Information | SGE | SLURM |
|--------------|-----|---------|
| Script directive | `#$` | `#SBATCH` |
| queue/partition | `-q $queue` | `-p $partition` |
| count of nodes  | N/A | `-N [min[-max]]` |
| CPU count | `-pe smp.q <count>` OR `-pe openmp <count>` | `-n <count>` |
| Wall clock limit | `-l h_rt=<seconds>` | `-t <min>` OR `-t <days-hh:mm:ss>` |
| stdout file | `-o <file_name>` | `-o <file_name>` |
| stderr file | `-e <file_name>` | `-e <file_name>` |
| combine stdout/stderr | `-j yes` | use `-o` without `-e` |
| copy environment | `-V` | `--export=(ALL/NONE/<variables>)` |
| event notification | `-m abe` | `--mail-type=<events>` |
| send notification email | `-M <address>` | `--mail-user=<address>` |
| job name | `-N <name>` | `--job-name=<name>` |
| Restart job | `-r (yes|no)` | `--[no-]requeue` (NOTE: configurable default) |
| set working directory | `-wd <dir_name>` | `--workdir=<dir_name>` |
| Resource sharing | `-l exclusive` | `--exclusive` OR `—shared` |
| Memory size | `-l mem_free=<memory>(K|M|G)` | `--mem[-per-cpu]=<memory>(K|M|G)` |
| Charge to an account | `-A <account>` | `--account=<account>` |
| Tasks per node | fixed rule in parallel environment (PE) | `--tasks-per-node=<count>` |
| Job dependency | `-hold_jid <job_id>` OR `-hold_jid=<job_name>` | `--depend=[<state>:]<job_id>` |
| Job project | `-P <name>` | `--wckey=<name>` |
| Job host preferences | `-q <queue>@<node>` OR `-q <queue>@@<hostgroup>` | `--nodelist=<nodes>` AND/OR `—exclude=<nodes>` |
| Quality of service | N/A` | `--qos=<name>` |
| Job arrays | `-t $array_spec` | `--array=$array_spec` |
| Generic Resources | `-l $resource=$value` | `--gres=<resource_spec>` |
| Licenses | `-l <license>=<count>` | `--licenses=<license_spec>` |
| Begin Time | `-a <YYMMDDhhmm>` | `--begin=<YYYY-MM-DD[THH:MM[:SS]]>` |
### Submit Scripts
<table><tr>
<th><big><center>SGE</center></big></th>
<th><big><center>SLURM        </center></big></th></tr><tr><td colspan="2">
<b>Single-core application</b>
</td></tr><tr><td><pre>
#!/bin/bash
#$ -N test
#$ -j y
#$ -o test.output
#$ -cwd
#$ -M $USER@sussex.ac.uk
#$ -m bea
##Request 5 hours run time
#$ -l h_rt=5:0:0

<call your app here>
</pre></td><td><pre>
#!/bin/bash 
#SBATCH -J test
#SBATCH -o test."%j".out
#SBATCH -e test."%j".err
#Default in slurm
#SBATCH --mail-user $USER@sussex.ac.uk
#SBATCH —mail-type=ALL
#Request 5 hours run time
#SBATCH -t 5:0:0
#SBATCH —mem=4000
#SBATCH -p general

<load modules, call your app here>
</pre></td></tr><tr><td colspan="2">
<b>MPI application with Multithreading</b>
</td></tr><tr><td>
</td><td><pre>
#!/bin/bash -l
#Standard output and error:
#SBATCH -o ./tjob.out.%j
#SBATCH -e ./tjob.err.%j
#Initial working directory:
#SBATCH -D ./
#Job Name:
#SBATCH -J test_slurm
#Queue (Partition):
#SBATCH --partition=general
#Number of nodes and MPI tasks per node:
#SBATCH --nodes=8
#SBATCH --ntasks-per-node=32
#
#Wall clock limit:
##Standard output, %A = job ID, %a = job array index
#SBATCH -o job_%A_%a.out
##Standard error, %A = job ID, %a = job array index
#SBATCH -e job_%A_%a.err
##Initial working directory:
#SBATCH -D ./
##Job Name:
#SBATCH -J test_array
##Queue (Partition):
#SBATCH --partition=general
##Number of nodes and MPI tasks per node:
#SBATCH --nodes=1
#SBATCH --ntasks-per-node=40
#
##Wall clock limit:
#SBATCH --time=24:00:00
##Run the program:
srun ./myprog > prog.out
</pre></td></tr><tr><td colspan="2">
<b>MPI Batch job using GPUs</b>
</td></tr><tr><td>
</td><td><pre>
#!/bin/bash -l
##Standard output and error:
#SBATCH -o ./tjob.out.%j
#SBATCH -e ./tjob.err.%j
##Initial working directory:
#SBATCH -D ./
#
#SBATCH -J test_slurm
##Queue:
##If using both GPUs of a node
#SBATCH --partition=gpu
##If using only 1 GPU of a shared node
###SBATCH --partition=gpu:A40:1
##Node feature:
#SBATCH --constraint="gpu"
##Specify number of GPUs to use:
# If using both GPUs of a node
#SBATCH --gres=gpu:A40:2
### If using only 1 GPU of a shared node
###SBATCH --gres=gpu:A40:1
#
##Number of nodes and MPI tasks per node:
#SBATCH --nodes=1
##If using both GPUs of a node
#SBATCH --ntasks-per-node=32
##If using only 1 GPU of a shared node
###SBATCH --ntasks-per-node=16
#
##wall clock limit:
#SBATCH --time=24:00:00
module load cuda
##Run the program:
srun ./my_gpu_prog > prog.out
</pre></td></tr>
</table>

<!--
### Tips & Tricks
#### Requeuehold
To keep track which jobs are actually failed or not inside the script.
```
scontrol requeuehold ${SLURM_JOB_ID}
```
And for an array job.
```
scontrol requeuehold ${SLURM_ARRAY_JOB_ID}_${SLURM_ARRAY_TASK_ID})
```
-->