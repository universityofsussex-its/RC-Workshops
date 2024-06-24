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

<ol>
<li> Simple file read </li>

```bash
#!/bin/bash
#$ -N Workshop_io
#$ -q smp.q
#$ -pe openmp 1
#$ -l m_mem_free=2G
#$ -l h_vmem=2G
#$ -cwd
#$ -j y
#$ -o output/workshop_io1
#$ -S /bin/bash
#$ -jc test.short

cat /its/home/<username>/penguin_names.txt | while read line
do
  echo $line
done
```

<li> Dynamic File Read </li>

```bash
#!/bin/bash
#$ -N Workshop_io2
#$ -q smp.q
#$ -pe openmp 1
#$ -l m_mem_free=2G
#$ -l h_vmem=2G
#$ -cwd
#$ -j y
#$ -o output/workshop_io2
#$ -S /bin/bash
#$ -jc test.short

cat $1 | while read line
do
  echo $line
done
```

```bash
qsub workshop_io.job /its/home/<username>/penguin_names.txt
```

<li> Creating and Destroying </li>

```bash
#!/bin/bash
#$ -N Workshop_cyberman
#$ -q smp.q
#$ -pe openmp 1
#$ -l m_mem_free=2G
#$ -l h_vmem=2G
#$ -cwd
#$ -j y
#$ -o output/workshop_cyberman
#$ -S /bin/bash
#$ -jc test.short

mkdir -p /mnt/lustre/users/<dep>/<user>/example1
mkdir -p /mnt/lustre/users/<dep>/<user>/example1/folder1
mkdir -p /mnt/lustre/users/<dep>/<user>/example1/folder2
mkdir -p /mnt/lustre/users/<dep>/<user>/example1/folder3
touch /mnt/lustre/users/<dep>/<user>/example1/folder2/afile1
touch /mnt/lustre/users/<dep>/<user>/example1/folder2/afile2
touch /mnt/lustre/users/<dep>/<user>/example1/folder3/afile1

```

```bash
#!/bin/bash
#$ -N Workshop_cyberman
#$ -q smp.q
#$ -pe openmp 1
#$ -l m_mem_free=2G
#$ -l h_vmem=2G
#$ -cwd
#$ -j y
#$ -o output/workshop_cyberman
#$ -S /bin/bash
#$ -jc test.short

mkdir -p /mnt/lustre/users/<dep>/<user>/example2
echo "made top level dir"
mkdir -p /mnt/lustre/users/<dep>/<user>/example2/folder1
mkdir -p /mnt/lustre/users/<dep>/<user>/example2/folder2
mkdir -p /mnt/lustre/users/<dep>/<user>/example2/folder3
echo "made sub folders"
touch /mnt/lustre/users/<dep>/<user>/example2/folder2/afile1
touch /mnt/lustre/users/<dep>/<user>/example2/folder2/afile2
touch /mnt/lustre/users/<dep>/<user>/example2/folder3/afile1
echo "made files"
sleep 60

echo "deleting files"
rm -y /mnt/lustre/users/<dep>/<user>/example2/folder2/afile1
rm -y /mnt/lustre/users/<dep>/<user>/example2/folder2/afile2
rm -y /mnt/lustre/users/<dep>/<user>/example2/folder3/afile1

echo "removing sub dirs"
rmdir /mnt/lustre/users/<dep>/<user>/example2/folder1
rmdir /mnt/lustre/users/<dep>/<user>/example2/folder2
rmdir /mnt/lustre/users/<dep>/<user>/example2/folder3

echo "removing top level"
rmdir /mnt/lustre/users/<dep>/<user>/example2
```

</ol>

<p align="right">(<a href="#top">back to top</a>)</p>

## Using SGE Variables

<ol>
<li> Simple User of SGE Variables </li>

```bash
#!/bin/bash
#$ -N Workshop_variables
#$ -q smp.q
#$ -pe openmp 1
#$ -l m_mem_free=2G
#$ -l h_vmem=2G
#$ -cwd
#$ -j y
#$ -o output/workshop_variables
#$ -S /bin/bash
#$ -jc test.short

cd $HOME
pwd
cd $SGE_O_WORKDIR

```

<li> Simple Host check </li>

```bash
#!/bin/bash
#$ -N Workshop_variables
#$ -q smp.q
#$ -pe openmp 1
#$ -l m_mem_free=2G
#$ -l h_vmem=2G
#$ -cwd
#$ -j y
#$ -o output/workshop_variables
#$ -S /bin/bash
#$ -jc test.short

cd $HOME
pwd
cd $SGE_O_WORKDIR
echo $SGE_O_HOST # or run the hostname command.
```

<li> Simple Core count chehck </li>

```bash
#!/bin/bash
#$ -N Workshop_variables
#$ -q smp.q
#$ -pe openmp 4
#$ -l m_mem_free=500M
#$ -l h_vmem=500M
#$ -cwd
#$ -j y
#$ -o output/workshop_variables
#$ -S /bin/bash
#$ -jc test.short

cd $HOME
pwd
cd $SGE_O_WORKDIR
echo $SGE_O_HOST # or run the hostname command.
echo $NSLOTS
```

<p align="right">(<a href="#top">back to top</a>)</p>

## Job Classes

<ol>
<li> Un-queueable job </li>

```bash
#!/bin/bash
#$ -N Workshop_jobclasses
#$ -q smp.q
#$ -pe openmp 2000
#$ -l m_mem_free=64G
#$ -l h_vmem=64G
#$ -cwd
#$ -j y
#$ -o output/workshop_jobclasses
#$ -S /bin/bash
#$ -jc verylong.default

cd $HOME
pwd
cd $SGE_O_WORKDIR
echo $SGE_O_HOST # or run the hostname command.
echo $NSLOTS
```


</ol>

<p align="right">(<a href="#top">back to top</a>)</p>

## Timed Jobs

<ol>
<li> Start Job After Timestamp </li>

```bash
qsub -a 202406231245 workshop.job # Note timestamp is just an example
```

<li> Start Job after Another Job completes </li>

```bash
#!/bin/bash
#$ -N Workshop_slow
#$ -q smp.q
#$ -pe openmp 2000
#$ -l m_mem_free=64G
#$ -l h_vmem=64G
#$ -cwd
#$ -j y
#$ -o output/workshop_slow
#$ -S /bin/bash
#$ -jc test.short

sleep 30
```

```bash
#!/bin/bash
#$ -N Workshop_waiting
#$ -q smp.q
#$ -pe openmp 2000
#$ -l m_mem_free=64G
#$ -l h_vmem=64G
#$ -cwd
#$ -j y
#$ -o output/workshop_slow
#$ -S /bin/bash
#$ -jc test.short

date +"%T"
```



</ol>


<p align="right">(<a href="#top">back to top</a>)</p>

## Extension Exercises

No Solutions Provided :P

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
