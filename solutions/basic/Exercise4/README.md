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
    <img src="../../../images/logo.png" alt="Logo" width="80" height="80">
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

```bash
#!/bin/bash
#$ -N Workshop_array
#$ -q smp.q
#$ -pe openmp 1
#$ -l m_mem_free=2G
#$ -l h_vmem=2G
#$ -cwd
#$ -j y
#$ -o output/workshop_array
#$ -S /bin/bash
#$ -jc test.short
#$ -t 11

echo $JOB_ID
echo $SGE_TASK_ID
echo $SGE_TASK_FIRST
echo $SGE_TASK_LAST
echo $SGE_TASK_STEPSIZE
echo $SGE_O_WORKDIR
echo $SGE_O_HOST
echo $SGE_O_WORKDIR
```

## Simple Itter Job

<ol>
<li> Simple Itter Job </li>

```bash
#!/bin/bash
#$ -N Workshop_itter
#$ -q smp.q
#$ -pe openmp 1
#$ -l m_mem_free=2G
#$ -l h_vmem=2G
#$ -cwd
#$ -j y
#$ -o output/workshop_simple_itter
#$ -S /bin/bash
#$ -jc test.short
#$ -t 1-25
#$ -tc 1

echo $JOB_ID
echo $SGE_TASK_ID
echo $SGE_TASK_FIRST
echo $SGE_TASK_LAST
echo $SGE_TASK_STEPSIZE
echo $SGE_O_WORKDIR
echo $SGE_O_HOST
echo $SGE_O_WORKDIR

sleep 1
```

</ol>

## Simple File Input Job

<ol>
<li> Directory Creation </li>

```bash
#!/bin/bash
#$ -N Workshop_array_io
#$ -q smp.q
#$ -pe openmp 1
#$ -l m_mem_free=2G
#$ -l h_vmem=2G
#$ -cwd
#$ -j y
#$ -o output/workshop_array_io
#$ -S /bin/bash
#$ -jc test.short
#$ -t 1-20
#$ -tc 20

mkdir -p "/mnt/lustre/users/<dep>/<username>/array_example/folder${SGE_TASK_ID}"
echo "/mnt/lustre/users/<dep>/<username>/array_example/folder${SGE_TASK_ID}" >> directory_paths.txt

```

<li> File Input </li>

```bash
#!/bin/bash
#$ -N Workshop_array_io
#$ -q smp.q
#$ -pe openmp 1
#$ -l m_mem_free=2G
#$ -l h_vmem=2G
#$ -cwd
#$ -j y
#$ -o output/workshop_array_io
#$ -S /bin/bash
#$ -jc test.short
#$ -t 1-20
#$ -tc 20

filepath=sed "${SGE_TASK_ID}q;d" directory_paths.txt

rmdir $filepath

```

<li> Stepping Stones </li>

```bash
#!/bin/bash
#$ -N Workshop_array_io
#$ -q smp.q
#$ -pe openmp 1
#$ -l m_mem_free=2G
#$ -l h_vmem=2G
#$ -cwd
#$ -j y
#$ -o output/workshop_array_io
#$ -S /bin/bash
#$ -jc test.short
#$ -t 2-20:2
#$ -tc 20

filepath=sed "${SGE_TASK_ID}q;d" directory_paths.txt

rmdir $filepath
```
</ol>

## Extension Exercises

No Solutions Provided :P


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