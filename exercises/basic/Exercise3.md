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
    <img src="../../images/logo.png" alt="Logo" width="80" height="80">
  </a>

  <h3 align="center">Basic Exercises #3</h3>
  <p align="center">
    This third set of exercies are to familairise yourself with using batch jobs to perform some of the actions you have aleady done, but without an interactive session.
  </p>
    <a href="https://github.com/universityofsussex-its/RC-Workshops"><strong>Go Back to Splash »</strong></a>
    <br />
</div>
<!-- TABLE OF CONTENTS -->
<details>
  <summary>Exercises</summary>
  <ol>
    <li><a href="#submit-a-simple-job">Submit a Simple Job</a></li>
    <li><a href="#file-operations">File Operations</a></li>
    <li><a href="#using-sge-variables">Using SGE Variables</a></li>
    <li><a href="#job-classes">Job Classes</a></li>
    <li><a href="#timed-jobs">Timed Jobs</a></li>
    <li><a href="#extension-exercises">Extension Exercises</a></li>
  </ol>
</details>

<p align="right">(<a href="#top">back to top</a>)</p>

## Submit A Simple Job

Submitting a job file when one is provided to you is a matter of copy and paste.

Either copy it from here - or locate it in the copied folder from the previous exercise (you'll need to locate it using `ls` and `cd` or create a file using `vim` - please name it `workshop.job`).

You will have to exit any interactive session. To check the server you are currently on you can use the `hostname` command.

<ol> 

<li> Simple Job </li>

<details>
<summary>Job File</summary>

```bash
#!/bin/bash
#$ -N Workshop_Basic
#$ -q smp.q
#$ -pe openmp 1
#$ -l m_mem_free=2G
#$ -l h_vmem=2G
#$ -cwd
#$ -j y
#$ -o output
#$ -S /bin/bash
#$ -jc test.short

echo $JOB_ID
echo $SGE_TASK_ID
echo $SGE_TASK_FIRST
echo $SGE_TASK_LAST
echo $SGE_TASK_STEPSIZE
echo $SGE_O_WORKDIR
echo $SGE_O_HOST
echo $SGE_O_WORKDIR
```

</details>


The arguments were described in the presentation part but for reference:

<ul>
<li> -N : Name of the job - will show in logs and scheduler queue </li>
<li> -l : Command to add additional consumable arguements. In this case "h_vmem" is the memory per core, and "m_mem_free" is the force available memory </li>
<li> -cwd : No value provided - is a flag to say please start the job in the submission current working directy as show by pwd command </li>
<li> -j y : Join both error and standard output into one file. If "n" will create a file named by jobname.o and jobname.e appended by jobid </li>
<li> -o : output file, if not specified defaults to the above. If a file, will append to it, if folder will create defaults files within </li>
<li> -S : Shell to execute the job script - as mentioned you can use other shells but here we will only be using bash </li>
<li> -jc : Specifies the job class - set usage limits and maximum cores etc. </li>
</ul>


Submit the file by running:

```bash
qsub workshop.job
```

And look at the newly created ``output`` file. Delete this file, create a directory called output and rerun the job. 

<li> Viewing the Queue </li>

  Given that the queue isnt too busy, our job should complete almost immediately.

  Lets put a `sleep` command into the job to get it to wait 10s before finishing. Use `man sleep` to find out how to use the command.

  Edit the job file to add the `sleep` command. 

  Once it has been submited run `qstat` and you should see your job either waiting or running in the queue, with details from the jobscript filling the queue information. 

  You can view the entire queue by selecting all users with the wildcard "*":

  ```bash
    qstat -u "*"
  ```

  This can be quite long and messy - considering piping to the `less` command, or filtering on the two queues relevant to you (smp.q and parallel.q)

  ```bash
    qsub -u "*" | less
    qsub -u "*" -q smp.q, parallel.q
  ```

</ol>

<p align="right">(<a href="#top">back to top</a>)</p>

## File Operations

<ol>
<li> Simple file read </li>

We can now start piecing some of the skills we've learnt in previous exercises to do file operations within a jobscript.

Copy the ``workshop.job`` file and name the copy ``workshop_io.job``.

Re-using your ``penguin_names.txt`` - modify ``workshop_io.job`` to read in the file and print the penguin names into the output file.
Rename the jobname to be ``workshop_io`` instead of ``workshop_basic``.
Submit your job and check it was successful.

<li> Dynamic File Read </li>
 
 Now modify the same jobscript file, but to take an argument fed from the commandline to read a given filename, like before.

 When submitting jobs this way, what do you think you need to be careful of?


<li> Creating and Destroying </li>

Create a new copy of ``workshop.job`` called ``workshop_cyberman.job``, and rename the job name accordingly.

When creating and deleting files and folders within a jobscript we need to be extra careful - particularly because using relative filepaths and wildcards can lead to huge losses of data.

Modify your ``workshop_cyberman.job`` to create the following file and folder structure in your lustre user space:

You should not be using relative paths - use full paths such as ``mkdir -p /mnt/lustre/users/its/anon123/example1/folder1`` not ``mkdir example1``.

```
\example1\
    \--->folder1
    \--->folder2
        \--->afile1
        \--->afile2
    \--->folder3
        \--->afile1
```

Run the job and double check the folder has been created and the structure looks like the above.

Modify your jobscript to then create the same structure but the top level is called ``example2``, and then <strong> safely </strong> remove the files and folders. Use a `sleep` command of sufficent length to see it was successful (eg 60s)

It might be worthwhile to put some useful `echo` commands to state the job has created the folders as it completes them and then deletes them.

</ol>

<p align="right">(<a href="#top">back to top</a>)</p>

## Using SGE Variables

<ol>
<li> Simple Use of SGE Variables </li>

Copy the ``workshop.job`` script and call it ``workshop_variables.job``.

Modify the script to change directory to your ITS home directory, print the current working directory command output and the change back to the jobscript working directory using the `$SGE_O_WORKDIR` and `$HOME` variables.

<li> Simple Host check </li>

Sometimes the job can go wrong, either because of an error in your script, a compute node failure, or a central Sussex IT failure. In general it is good to write the host name of the compute node you're job is running on. This way, in the event of failure which you believe is a fault with the system, you can provide the node your job was running on.

Modify your jobscript to write the hostname of the compute name your jobs is sent to. 

<li> Simple core count check </li>

Modify your jobscript to ask for 4 cores and only 500MB of RAM per core. Output the number of cores your job was assigned (`$NSLOTS`) to the output file.

</ol>


<p align="right">(<a href="#top">back to top</a>)</p>

## Job Classes

In order to make the HPC and scheduler as fair as possible, we use job classes to limit runtimes and number of cores which can be consumed by those jobs.

This is in an attempt to prevent a user on a quiet night, hogging the entire cluster for 2 weeks...

There are two types of jobclasses:

<ol>
  <li> verylong.default </li>
  This is the default class given if you forget to set it. It is the longest running and most constraining on maximum number of jobs/cores in use. Try not to use it. Kills your job if it takes longer than 30 days.
  <li> test </li>
    <ul>
      <li> test.short </li>
      Shortest and most numerous cores. Kills your job if it runs longer than 2h.
      <li> test.default </li>
      Midlle ground - Kills your job if it takes longer than 8h.
      <li> test.long </li>
      More contraining on cores but allows the job to run for a maximum of 8 days. 
    </ul>
</ol>

As such - if you have a long running job it is recommended you impliment checkpointing into your code. This will allow you to run with more cores competitively and simply resume where the previous run ended.

<li> Un-queuable Job </li>

Copy and create a new jobscript called ``workshop_jobclasses.job``.

Modify the script so the jobclass is ``verylong.default`` and request 2000 cores and 64GB per core. 

Submit the job and check its status in the queue. 

Unfortuantely this job will never run, so we need to delete it.

In the output of the `qstat` command, your `jobid` will have been listed. Using that jobs id, submit the command:

```bash
qdel <jobid>
```

<li> Modifying a Queued Job </li>

If you set the job class correct, you might realise that you submitted the wrong number of cores in your jobscript, or on the command line. You can modify your job once its been submitted with the `qalter` command. You cannot change the job class.

Submit the job above again.

Either from the command line output when you submitted the job, or using `qstat` to get the jobid. 

Change the number of requested cores to 1 and RAM to 2GB.

```bash
qalter <jobid> -pe openmp 1 -l h_vmem=2G -l m_mem_free=2G
```

The job should now sucessfully queue, and the terminal should state which config options for the job it has had to change.

You cannot change runtime or jobclass via this method as they are controlled by the shedular submission wrapper.


<p align="right">(<a href="#top">back to top</a>)</p>

## Timed Jobs

For ecological reasons you might want to submit a job to run overnight, or after a specfic time. And example might be a job which needs to run after another remote system has updated (eg. Downloading Data after a public release). Another option is to run at time when the UK energy grid is most green/expected to be most green. Or if your job is dependendent on another job having completed (technically errored, failed and killed will also count as completed on the Apollo2 Grid Engine)

<li> Start Job After Timestamp</li>

To do this you can set the `-a` flag, short for after. 

The format for this is in three forms:

```bash
qsub -a 12241200 workshop.job # December 24th at 12:00.00
qsub -a 202412241200 workshop.job # December 24th 2024 at 12:00.00
qsub -a 202412241200.30 workshop.job #December 24th 2024 at 12:00 and 30 seconds.
```

For ease of eyesight - we can expand the long variable out: `2024-12-24-12-00.30`.

Submit a previous job while setting this commandline flag - set it to be 1 minutes after you submit and check back to see if it completed when you expected. 

You can look at past jobs that have completed with the `qacct -j <jobid>` command.


<li> Start Job After another Job completes </li>

Copy and create two new jobscript files called ``workshop_slow.job`` and ``workshop_waiting.job``.

Modify the first jobfile to be a simple sleep job for 30seconds. Have it print the start time to the output file using the `date +"%T"` command. The second ``workshop_waiting.job`` can be any of your previous jobscripts. Add a similar time statement out to the log file.

Now you can submit both jobs in sequence, with a requirement the the first job must be completed before the second starts. Here we make use of the " -terse" argument to `qsub` so that it only returns the ``jobid``.

```bash
jobids=$(qsub -terse workshop_slow.job)
jobids=jobids,$(qsub -terse workshop_slow.job) # Repeated to demonstrate a hold for multiple jobs
qsub -hold_jid ${jobids} workshop_waiting.job
```

Check the status of the queue and the sequence of timestamps to confirm the order once all your jobs have completed.


<p align="right">(<a href="#top">back to top</a>)</p>

## Extension Exercises

These are extension exercises if you wish to spend more time learning the more advance features of the grid engine batch scheduler. Support for these is not provided for you, and solutions will be self evident of reaching the requested result. 

Each of these tasks are completeable with the skills you have developed over these three exercies so far. However you may need to investivate more with `--help` and `man`. 

<li> Sequential Fibonacci Sequence </li>

Create a jobscript which calculates the Fibonacci sequence by matching the following conditions.
<ol>
<li> Calculates 100 Fibonacci numbers and writes them to a file - Job then completes </li>
<li> If a previous job has calculated 100 Fibonacci numbers, read the last two numbers in the file and calculate the next 100 </li>
<li> If the job were to go beyond 1k Fibonacci numbers, it only returns the next 25 , and then stops. </li>
<li> The job sleeps for 30 second after calculting its 100 numbers </li>
<li> The submit time for all of the jobs need to be within 1 minute (submit time is the time when the job is sent from command line, start time is when the job starts)</li>
</ol>

<li> GPU Job </li>

For this you will need to submit a job which reserves a single gpu_card, runs the `nvidia-smi` command and stores the results to a log file. This log file should also provide the date and time the command was run, which node it was run on and the directory the job was submitted from.

<li> Environment Creater </li>

Create a jobscript which will automatically load at least 30, non-conflicting, same tool-chain modules for a user. It will then save that module set for the user. This jobscript should only run after midnight of the next day of the jobs submission to reduce carbon footprint.




<p align="right">(<a href="#top">back to top</a>)</p>


<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
[contributors-shield]: https://img.shields.io/github/contributors/universityofsussex-its/RC-Workshops.svg?style=for-the-badge
[contributors-url]: https://github.com/universityofsussex-its/RC-Workshops/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/universityofsussex-its/RC-Workshops.svg?style=for-the-badge
[forks-url]: https://github.com/universityofsussex-its/RC-Workshops/network/members
[stars-shield]: https://img.shields.io/github/stars/universityofsussex-its/RC-Workshops.svg?style=for-the-badge
[stars-url]: https://github.com/universityofsussex-its/RC-Workshops/stargazers
[issues-shield]: https://img.shields.io/github/issues/universityofsussex-its/RC-Workshops.svg?style=for-the-badge
[issues-url]: https://github.com/universityofsussex-its/RC-Workshops/issues
