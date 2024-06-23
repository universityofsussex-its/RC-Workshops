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

  <h3 align="center">Basic Exercises #1</h3>
  <p align="center">
    This first set of exercise will introduce you to navigating around the HPC, from your Home directory to storage systems, creating a bash script and lastly creating a copy of this repository.
  </p>
    <a href="https://github.com/universityofsussex-its/RC-Workshops"><strong>Go Back to Splash »</strong></a>
    <br />
</div>
<!-- TABLE OF CONTENTS -->
<details>
  <summary>Exercises</summary>
  <ol>
    <li><a href="#login">Login</a></li>
    <li><a href="#basic-bash">Basic Bash</a></li>
    <li><a href="#storage">Storage</a></li>
    <li><a href="#storage">Bash Scripts</a></li>
    <li><a href="#storage">Summary</a></li>
  </ol>
</details>

<p align="right">(<a href="#top">back to top</a>)</p>



<!-- Login -->
## Login
<p>
  This first exercise will get you logged into the Apollo2 HPC. You will enter the <strong>Janus</strong> login node. Traditionally this login node is not for any work, but for navigating around and editing scripts.
</p>
<p>
  Please go to whatever OS you use, then proceed to <a href="#all">ALL</a> section.
</p>

### Mac

##### Start a terminal
Click <b>Launchpad</b> >> <b>Terminal</b>
Ths should bring up a black bash shell terminal. This will allow you to run the ssh login commad to janus:

```
  ssh -XY <username>@janus.hpc.sussex.ac.uk
```

Where <it>username</it> is your sussex, shortform username for email/canvas etc. Eg.

```
  ssh -XY anon123@janus.hpc.sussex.ac.uk
```

### Linux

Generall the shortcut `Ctrl + Alt + T` will open a terminal window for you.

Ths should bring up a purple,red or black bash shell terminal based on your flavour of linux. 

This will allow you to run the ssh login commad to janus:

```
  ssh -XY <username>@janus.hpc.sussex.ac.uk
```

Where <it>username</it> is your sussex, shortform username for email/canvas etc. Eg.

```
  ssh -XY anon123@janus.hpc.sussex.ac.uk
```

### Windows

For connecting to the HPC - this workshop will only provide one example using MobaXterm. The reason for this is simple - the RC admin who wrote this likes MobaXterm... :D 

Launch MobaXterm from the Search Window or from your Desktop (we suggest to pin to taskbar if you will use the HPC often)

You should get a window open like this:
<img src="images/exercise1/a2-mob1.png">

Click <strong>Session</strong> in the top left corner. You should have a window pop up that looks like this:
<img src="images/exercise1/a2-mob2.png">


Click <strong>SSH</strong> in the top left again and enter the following:

Remote host: `janus.hpc.sussex.ac.uk`
Username: `anon123`

Where the username is your sussex, shortform username for email/canvas etc.

It should look like this:
<img src="images/exercise1/a2-mob3.png">

Click <strong>OK</strong> and you will open a terminal in the main MobaXterm window, which will prompt for your Sussex password. Type this in, noting that you will not see the cursor move/show your password. (Fun tidbit - this was orignally a bug in linux but was thought useful and kept).


### ALL

You should now be seeing the Login Splash for the Apollo2 HPC. Depending on your terminal theme it should look somthing like this:

<img src="images/exercise1/a2-splash.png">

<strong>IF</strong> you cannot connect to `janus.hpc.sussex.ac.uk` you can try our second, older login node `apollo2.hpc.sussex.ac.uk`.

If you get banned from Janus due to weird activity trying to login (or password failure too many times) - contact an admin with your ip address to be unbanned. Visit <a href="www.sussex.ac.uk/its/ip">here</a> if you need to find your IP. (Preferred route as this says what Sussex sees your IP as).


## Basic Bash

<ol>
<li><h3> man Command</h3></li>

  One of the most usefull tools available for figuring out bash and other commands while you are on the HPC is the `man` command. This will bring up a text manual for whichever command you want to check. You may never stop using it, even after 10 years... It is very handy when you have forgetten which way around arguments go for a given command. 

  This exercise will use a number of commands, which you should first check with the man command to figure out how to use it. 

  This first question requires you to use the `man` command on the `ls` or list function for a directory.

  ```
    man ls
  ```

<li><h3> List your home directory</h3></li>

   So assuming you havent already moved about - you should be in your home directory - you can check this with the "print working directory command" `pwd`.

   Having now viewed the manual for `ls` command, please list your home directory with the following flags:
   <ul>
     <li>human-readable</li>
     <li>long listing format</li>
     <li>Reverse Order while listing</li>
     <li>Sort by modification time, newest first</li>
   </ul>

<li><h3> Create a Folder </h3></li>

  I would like to to create a new folder in your home directory called ``example1``, using the `mkdir` command. Please use `man mkdir` to see how to do this.
  
  Now re-list your home directory after that command has run to see the change when creating that folder.

<li><h3> Change Directory</h3></li>
   
   This command is the bread and butter of navigating the HPC. The command is "change directory" `cd`. Using the `man` command, look into how to change directories and descend into your newly created folder ``example1``.

<li><h3> Create a File</h3></li>

   We will now create an empty file, ready to be written to. This uses the `touch` command. Please create a file called ``afile.txt`` in your ``example1`` directory. (Again, use man to find out how to use the command)

<li><h3> Write to a File</h3></li>

   Using command line operations only, we will now write to, and append to the new file you have created.
   Using the `echo` command, we will write and forward the outputs into the file. The first using the overwrite operator `>>` and the seccond using the append operator `>`.

   Please add the following two lines to ``afile.txt``:
   <ul>
     <li> This should appear inside the file </li>
     <li>This should be the second line in the file</li>
   </ul>

   <details>
     <summary>Hint</summary>
       <ul>
         <li> echo "Beep boop" >> robot.txt </li>
       <ul>
    </details>

<li><h3> View a File</h3></li>
  
  Given that you were successful in writing to the file - if not, copy the hint from above to complete this question.

  There are multiple ways to view files in the bash shell command line environment.

  `cat` Is a command to print the contents to the command line. Use `man cat` to see how and check to see if you correctly wrote to the file in the previous step.

  `less` Is a command, useful if you want to keep your command line clear/not print large files out to the command line. Again using man, view the file with the `less` command.

  `vim` Is a command line editor. View the manual with `man vim`. It can be tricky - even unix admins for years screw up and have to force exit vim...

  Generally:
  <ul>
    <li> i: Will begin Interactive mode once vim is open to allow you to edit</li>
    <li> esc: exits most modes, including interactive </li>
    <li> ":" The colon begins the command window - used mostly to exit once edits are done, and save, force quit etc.</li>
    <li> "wq" : is the "write and quit" command to be used with the return key when in command mode. </li>
    <li> "q!" : is the "oops" force quit command when in the command mode </li>
  </ul>

  Please try editing ``afile.txt``, and the saving your results with vim. View with `less`, if its made an changes.

<li><h3> Delete a File</h3></li>
   
   The dangerous command `rm`. Please be careful here - recovering a home directory is an absolute pain to do during a workshop...

   Using `man` have a look at the `rm` command, and when comfortable, delete ``afile.txt``.

<li><h3> Delete a Folder</h3></li>
 
  Now we can use a safer command `rmdir` which will only delete empty directories. 

  View the manual for `rmdir`, and after changing directory back to your home directory, or ascending up one level, delete ``example1`` dir.
</ol>




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
