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

  <h3 align="center">Basic Exercise Solutions #1</h3>
  <p align="center">
    This first set of exercise will introduce you to navigating around the HPC, from your Home directory to storage systems, creating a bash script and lastly creating a copy of this repository.
  </p>
    <a href="https://github.com/universityofsussex-its/RC-Workshops"><strong>Go Back to Splash »</strong></a>
    <a href="https://github.com/universityofsussex-its/RC-Workshops/exercises/basic/exercise1.md"><strong>Go Back to Exercises »</strong></a>
    <br />
</div>
<!-- TABLE OF CONTENTS -->
<details>
  <summary>Exercises</summary>
  <ol>
    <li><a href="#basic-bash">Basic Bash</a></li>
    <li><a href="#storage">Storage</a></li>
    <li><a href="#storage">Bash Scripts</a></li>
    <li><a href="#storage">Summary</a></li>
  </ol>
</details>

<p align="right">(<a href="#top">back to top</a>)</p>

## Basic Bash

<ol>
<li><h3> man Command</h3></li>

  ```
    man ls
  ```

<li><h3> List your home directory</h3></li>

  ```
    ls -lthr
  ```

<li><h3> Create a Folder </h3></li>

  ```
    mkdir /its/home/<username>/example1
  ```
  ```
    ls -lthr
  ```

<li><h3> Change Directory</h3></li>

  ```
    cd /its/home/<useranme>/exmaple1
  ```
  ```
    pwd
  ```

<li><h3> Create a File</h3></li>

  ```
    touch afile.txt
  ```
  ```
    ls -lthr
  ```

<li><h3> Write to a File</h3></li>

  ```
    echo "This should appear inside the file" >> afile.txt
  ```
  ```
    echo "This should be the second line in the file" > afile.txt
  ```
<li><h3> View a File</h3></li>

  ```
    cat afile.txt
  ```
  ```
     less afile.txt
  ```
  Press `q` to quit.
  ```
    vim afile.txt
  ```
  Press `esc` and then `wq` to write and quit. To quit with no changes, use `q!`.

<li><h3> Delete a File</h3></li>

  ```
    rm /its/home/<username>/example1/afile.txt
  ```
  ```
    ls -lthr
  ```

<li><h3> Delete a Folder</h3></li>

  ```
    cd ../
  ```
  ```
    rmdir example1
  ```
  ```
    ls -lthr
  ```

</ol>