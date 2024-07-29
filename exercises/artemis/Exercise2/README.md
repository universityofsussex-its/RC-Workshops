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

  <h3 align="center">Artemis Exercises #2</h3>
  <p align="center">
    This second set of exercise will get you logged into the Open OnDemand Web Portal and exploring.
  </p>
    <a href="https://github.com/universityofsussex-its/RC-Workshops"><strong>Go Back to Splash »</strong></a>
    <br />
</div>
<!-- TABLE OF CONTENTS -->
<details>
  <summary>Exercises</summary>
  <ol>
    <li><a href="#job-composer">Job Composer</a></li>
    <li><a href="#job-from-template">Job From Template</a></li>
    <li><a href="#repair-templates">Repair Templates</a></li>
    <li><a href="#saving-your-work">Saving Your Work</a></li>
  </ol>
</details>

<p align="right">(<a href="#top">back to top</a>)</p>


## Job Composer

The Job Composer is the Open OnDemand clicky button GUI for users not familiar with command line or prefer to use applications outside of Emacs, Vim etc. to edit files. The execution status, templating and other tools will allow laymen users to make basic use of the cluster. For more advanced users, the templating and options available will allow better tracking of multiple job runs and results, and the ability for admins to better assist with problems compared to Apollo2 and SGE.

Exercises:

1. Navigate to the Job Composer. 
    
    Depending on the progress of other attendees you will see the default two jobs, and potentially some other users job scripts.

2. Navigating to Templates

    By default - the navigation bar at the top should have changed colour and show two tabs:
    - Jobs
    - Templates

    These tabs will allow you to switch between Job Templates, which you can create jobs from, and the Jobs editor.

    To navigate back to the Dashboard - click Open OnDemand in the top left.


<p align="right">(<a href="#top">back to top</a>)</p>

### Job From Template

In this section the exercises will take you through the job composer and the use of templates to create, edit and submit new jobs.

3. Create a new job.

    From the `New Job` dropdown button - select "From Template". This will navigate you to the "Templates" tab.

    Click/Select the `RES-Workshop-Empty` Template - which should show on the right under Job Name.

    Rename the job to something unique and easy for you to find in a list. Your Sussex username is Suggested. eg. `<username>-Empty`.

    Click `Create New Job`.

    You should now be back on the Jobs page instead of templates. with a new job with its details highlighted on the right.

    You should be able to see that the folder contains a single job file, which is empty beside a print statement.
1. Submit a Job
    Run your new job by selecting it in the list of jobs (you might need to use the search bar) and clicking "Submit".

    If the Queue is busy - its will change status to queues. 
    It should run almost instantaneously and be marked as Completed.

1. Check Job Results

    Once your job completed, reselect it in the jobs if need be and look at the folder contents.

    Although the job file was mostly empty, Artemis attempted to populate some defaults for you.

    Click the `slurm-<job_id>.out` file and view the results.

    Navigate back to your job page.

1. Editing the Job Script

    Click the `main_job.sh` file to begin editing it.

    Please, either using slides, google or the cheat sheat, set the SBATCH job headers to complete the following job. 
    
    - `general` Partition.
    - Request one CPU.
    - `250mb` of total RAM
    - No Mailing Options
    - Max runtime of 5 minutes
    - One file for stdout and another stderror with the following naming format:
        - `jobname-<jobid>.<out,err>`
    - Outputs the hostname, current working directory and the date on job start.
    - Outputs the jobnumber from the environment variable.
    

    If you get stuck - check the other default templates for ideas.

    Submit the job to check your results.

6. Changing the Job File

    Open your job script directory using the button in the very bottom right corner.

    Create a new file `my_slurm_job.job` as a copy of `main_job.sh`.

    Now go back to the Jobs Composer, Select your Job, and click `Job Options`.

    This menu will allow you to:
    - Rename your Job
    - Change submit Cluster (You only have prd available)
    - Change the Job Script Submitted
    - Set the account (not needed)
    - Set the array args
    - Copy your submit environment

    Please switch the job script to `my_slurm_job.job` and set the array arg to `1-4:2%1`.

    Save your changes and edit your job to also output the Min, Max and Current task number to stdout. 

    You should notice that you now have `Job Array Request:` as a new field when viewing the job.

    Submit the job and check it ran successfully.


<p align="right">(<a href="#top">back to top</a>)</p>

### Convert Templates

This section you will create jobs from default templates and attempt to repair/convert them. Each exercise will have a number of errors and a description of what the template was meant to do. 

Each Exercise should start by you creating a new job from the template, copying the default job script into a new script and correcting issues.

8. SGE to SLURM SMP

    - Template: `SGE-SLURM-OpenMP`
    - Description:
        A simple multithread python execution

1. SGE to SLURM MPI

    - Template: `SGE-SLURM-MPI`
    - Description: A Simple 2 proc MPI job.


1. No Route
    
    - Template: `SGE-SLURM-wget`
    - Description: A simple Job to fetch some files from the web.

        <details>

        <summary>Hint</summary>

            wget -e use_proxy=on -e https_proxy=$HTTPS_PROXY

        </details>

<p align="right">(<a href="#top">back to top</a>)</p>

## Saving Your Work

Please now open your jobs directoires which you have created and copy them over to your `workdir` your created in the previous Exercise Sheet.

When you delete a job in the Job Composer - it wipes the directory, job script and all results contained within.

<p align="right">(<a href="#top">back to top</a>)</p>

## Summary

These series of exercises should have familiarsed yourself with the following:

- Jobs:
    - Submission
    - Templates
    - Creation
    - Editing
    - Reviewing
    - Job Options
    - Saving
- SGE to Slurm Conversions
    - SMP or Open MP Jobs
    - Open MPI and the ease of Ranks/node
    - Proxies and the changes in default behaviour


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