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

  <h3 align="center">Basic Exercises #4</h3>
  <p align="center">
    This set of exercises are designed to introduce you to array jobs. These are when you need to process a large number of objects/timesteps or sequences of data that will use the same pipeline but will vary with input parameters or filenames.
  </p>
    <a href="https://github.com/universityofsussex-its/RC-Workshops"><strong>Go Back to Splash »</strong></a>
    <br />
</div>
<!-- TABLE OF CONTENTS -->
<details>
  <summary>Exercises</summary>
  <ol>
    <li><a href="#basic-array-job">Basic Array Job</a></li>
    <li><a href="#simple-itter-job">Simple Itter Job</a></li>
    <li><a href="#simple-file-input-job">Simple File Input Job</a></li>
    <li><a href="#extension-exercises">Extension Exercises</a></li>
  </ol>
</details>

<p align="right">(<a href="#top">back to top</a>)</p>

## Basic Array Job

We will now introduce a slight change on the batch job. The syntax is exactly the same as you have used with batch jobs, but there are two additional arguements and four new job variables availible within the jobscript to use.



We will be introducing two new flags. The "task" arguemnt `-t` and the max concurrent tasks flag `-tc`.

<ul>
<li> "-t start-stop:step" Arguement is a generator of a number squence usable within the array jobscript. </li>
<li> "-tc int" Arguement limits the number of tasks that the array job will allow to be run at once. This is to prevent 100's of lightweight jobs jumping priority and not allowing fair use of the HPC resources. We generally ask for a maximum of 250 cores of concurrent tasks. </li>
<li> "$SGE_TASK_ID" is the generated task id from the start-stop:step generated from the -t argument. Useful for grabbing specic lines in databases or files. </li>
<li> "$SGE_TASK_FIRST" Is the value provided to the -t argument for start. </li>
<li> "$SGE_TASK_LAST" Is the value provided to the -t argument for stop OR maximum allowed with the given step size. </li>
<li> "$SGE_TASK_STEPSIZE" Is the value provided to the -t argument for the stepsize. </li>
</ul>

It is important to note that the defaults for this are:

```bash
-t 25    # Will only run 1 job like a batch job but the variables will be set that the SGE_TASK_ID is 25
-t 1-30  # Will defatul step size to 1 and run 30 tasks from 1,2...,29,30.
```

<ol>
<li> Array Job Variables </li>

Copy and modify the ``workshop.job`` into an array job, which also prints the 4 new environment varibales to the output file. Call this file ``workshop_array.job``. Run a single task for the array job for `TASK_ID=11`.
</ol>

<p align="right">(<a href="#top">back to top</a>)</p>

## Simple Itter Job

<li> Array Job Concurrency </li>

If you set concurrency to 1, you can generate a large array of jobs which will attempt to run consecutively. Modify you array jobscript to run 25 jobs consecutively.

<p align="right">(<a href="#top">back to top</a>)</p>

## Simple File Input Job

<li> Directory Creation </li>

Create an array job which will iteratively create 20 folders, and write the full folder paths to a file ``directory_paths.txt``, one on each line. Each task should create its own folder.

<li> File Input </li>

Create a new array job (you'll need to rerun the previous script again later so don't modify it) to delete the newly created folders. Each task should use its TASK ID to read the ``directory_paths.txt`` without knowing or using the folder structure you created. (IE, dont cheat, use the paths created)

<li> Stepping Stones </li>

Submit an array job to recreate 20 folders again with different names to the ones you chose previously (There is a step you'll need to do before running the script...what is it? If unsure, proceed anyway and look at the error messages.). This time create an array job to delete every even row numbered folder in ``directory_paths.txt``. (eg lines 2,4,6,8,10).

To grab a specific line in a file you can use `sed "<row_num>q;d" inputfile`. 

<details>
<summary>Hint</summary>

```bash
filepath_to_delete=$(sed "${SGE_TASK_ID}q;d" directory_paths.txt)
```

</details>

<p align="right">(<a href="#top">back to top</a>)</p>

## Extension Exercises

These are extension exercises if you wish to spend more time learning the more advance features of the grid engine array scheduler. Support for these is not provided for you, and solutions will be self evident of reaching the requested result. 

Each of these tasks are completeable with the skills you have developed over these four exercies so far. However you may need to investivate more with `--help` and `man`. 

<li> Sequential Fibonacci Sequence </li>

Create an array jobscript which calculates the Fibonacci sequence by matching the following conditions.
<ol>
<li> Calculates 100 Fibonacci numbers and writes them to a file - Job then completes </li>
<li> If a previous job has calculated 100 Fibonacci numbers, read the last two numbers in the file and calculate the next 100 </li>
<li> If the job were to go beyond 1k Fibonacci numbers, it only returns the next 25 , and then stops. </li>
<li> The job sleeps for 1 second after calculting its 100 numbers </li>
</ol>

<li> Itemize and descned a directory </li>

For the RC-Workshops folder you copied into you lustre directory, write a <strong>batch</strong> job that;

Starting at the top level directory, lists all the files and folders and writes them their paths to a file. It then descends into each folder and repeats.

And then create an array job that:
<ol>
<li> Iterates through that created file full of paths </li>
<li> Takes a single path, and writes to another file, its output from `ls -lthr`</li>
<li> Uses the "wc" command to find how many characters, words and line are in the file and outputs that to a new file </li>
<li> The last array task deletes the original input file of paths from the previous batch job </li>
</ol>

Run both jobs such that the first task of the array job waits for the first batch job to complete.


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
