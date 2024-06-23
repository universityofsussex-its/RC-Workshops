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
    <img src="images/logo.png" alt="Logo" width="80" height="80">
  </a>

  <h3 align="center">Basic Exercise Solutions #3</h3>
  <p align="center">
  </p>
    <a href="https://github.com/universityofsussex-its/RC-Workshops"><strong>Go Back to Splash »</strong></a>
    <a href="https://github.com/universityofsussex-its/RC-Workshops/exercises/basic/exercise1.md"><strong>Go Back to Exercises »</strong></a>
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


## Submit a Simple Job

<ol>
<li> Viewing the Queue </li>
  <details>
  <summary> Jobscript </summary>

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
  echo $SGE_O_WORKDIR
  echo $SGE_O_HOST
  echo $SGE_O_WORKDIR

  sleep 10
  ```

</details>
</ol>


## File Operations

Some example of pushing



<p align="right">(<a href="#top">back to top</a>)</p>

## Using SGE Variables

<p align="right">(<a href="#top">back to top</a>)</p>

## Job Classes

<p align="right">(<a href="#top">back to top</a>)</p>

## Timed Jobs

<p align="right">(<a href="#top">back to top</a>)</p>

## Extension Exercises

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
