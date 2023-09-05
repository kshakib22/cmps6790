---
layout: page
title: Project 0
subtitle: Setting Up The Computing Environment
published: true
---

# Project 0: Computing Environment

* **Posted:** August 23, 2023
* **Last Revision:** August 23,2023

Over the course of the semester, you will work with a variety of software packages, including Python, Pandas, Jupyter Notebook, and others. Installing those packages and getting started can often be a hassle because of software dependencies.  *However, maintaining your environment is an integral part of your job as a data scientist so you'll need to get used to it!  Luckily Docker makes this really easy and also allows you to share runnable code and increase reproducibility!*

For this class we will use Docker, as discussed below. If you have a reasonably modern machine, within last 3-4 years, this should generally work fine, but with older laptops, the performance may not be as good. See below for more details on this.

---

## Git & Github

Git is one of the most widely used version control management systems today, and invaluable when working in a team. GitHub is a web-based hosting service built around git that supports hosting git repositories, user management, etc. There are other similar services, e.g., BitBucket and GitLab.

We will use GitHub to distribute the assignments, and other class materials. Our use of git/github for the class will be minimal; however, we encourage you to use it for collaboration for your class project, or for other classes, or for anything because it's great.

If you are uncomfortable with the command line interfaces below you can try a variety of IDEs that are designed to make this easier.

* I personally use [VS Code](https://code.visualstudio.com/) because it is a really nice, fully integrated development environment that can manage Docker, Python, Git, and many more things -- you should try it!
* The [GitHub Desktop](https://desktop.github.com/) is also a popular choice and is very easy to use. 
* I used to use [SourceTree](https://www.sourcetreeapp.com/), though it is a bit more advanced and may have lots of options you do not need for this course.

If you have a Windows machine then I highly suggest using one of these, if you have a Mac, the git command line is pre-installed on your computer.

### (Less Preferred) Just Cloning the Class Repository

You don't need a GitHub account for just cloning the class repository. From the command line, just do:

`git clone https://github.com/nmattei/cmps6790.git`

You can do `git pull` (from within the `cmps6790` directory) to fetch the newly added material. 

*NOTE*: If you are having trouble installing `git`, you can just download the files instead (as a zipfile), although updating may become tedious. 

### (More Preferred) Setting up a GitHub Account

Repositories hosted on github for free accounts are public; however, you can easily sign up for an educational account which allows you to host 5 private repositories. More details at [GitHub Education Accounts](https://education.github.com/).

To do this you need to follow these steps:

1. Create an account on Github: https://github.com
2. Generate and associate an SSH key with your account
    * [Instructions to generate SSH Keys](https://docs.github.com/en/authentication/connecting-to-github-with-ssh)
    * Make sure to remember the passphrase or leave it blank (less secure).
    * Go to your [GitHub Profile](https://github.com/settings/profile), and find the add SSH Keys link.
    * Add your SSH Keys which can be found following the above tutorial on generating your SSH keys.
3. Clone the class repository:
    * In Terminal: `git clone git@github.com:nmattei/cmps6790.git`
    * The master branch should be checked out in a new directory 
4. Familiarize yourself with the basic git commands.
    * At a minimum, you would need to know: `clone`, `add`, `commit`, `push`, `pull`, `status`.
    * But you should also be familiar with how to use **branches** (we will discuss these in class).
5. You can't push to the main class repository, but feel free to do *pull requests* on the main class repository if you spot any errors or if you think something could be improved.
6. **Important Note!!** I strongly suggest doing your work in another location on your local machine or even private git repository. If I make updates to the course git and you need to `git pull` again, and you have edited the files locally, you will have to `stash` your changes or you'll have lots of conflicts!

**HINT HINT:** Pay attention to where in your computer you are cloning the directory.  We are going to need this later.  On Mac/Linux you can use the command `pwd` from the command line to see what the `PATH` is to your current directory.  For example, mine says `/Users/nsmattei/repo/teaching/cmps6790`.

---

## Docker

Docker is a software technology providing `containers`, that provides an additional layer of abstraction and automation of operating-system-level `virtualization` on Windows and Linux. [Here is a nice introductory blog post that describes virtualization and containers](https://medium.freecodecamp.org/a-beginner-friendly-introduction-to-containers-vms-and-docker-79a9e3e119b).

Briefly speaking, a virtual machine (VM) is an emulation of an (`guest`) operating system on a computer (with potentially a different `host` operating system). Linux is the most common guest OS that is used, especially since Apple and Microsoft make it difficult to emulate their OSes. `Containers` look like a VM, but share the host kernel (if possible) to be more efficient, both in terms of the memory used and the slowdown.

Docker is perhaps the most popular container technology at this time, and is widely used to package and ship applications. There are many pre-existing `images` that can be pulled from [Docker Hub](https://hub.docker.com/) (or elsewhere) to quickly install and run different software (as you will see below).

To install Docker Desktop you should do the following.

1. To get started, install Docker Desktop (note, not Docker Engine!) by following the instructions on the [webpage for your machine type](https://docs.docker.com/get-docker/).
2. Follow the appropriate `Getting Started` guide to make sure that Docker is working as expected.
    * [For a Mac](https://docs.docker.com/desktop/install/mac-install/)
    * [Windows](https://docs.docker.com/desktop/install/windows-install/)
    * **Note:** If you have Windows 10 Home you need to use [Docker Toolbox](https://docs.docker.com/toolbox/toolbox_install_windows/) which you can find the installation instructions for here: .  If you are having trouble mounting your filesystem in Docker Toolbox for Windows please go over [this troubleshooting guide](https://medium.com/@Charles_Stover/fixing-volumes-in-docker-toolbox-4ad5ace0e572).
    * **Note:** On Windows if you get the error *Error: invalid reference format: repository name must be lowercase.* then this means that you need to change the `PATH` below to not have any spaces. This may involve moving the folder you want to map.
    * We will use the [Jupyter Notebook Data Science Stack](https://hub.docker.com/r/jupyter/datascience-notebook/) to get started in this class. You can start it using the following command in the command line -- **replace PATH with the path to where you have saved or checked out the git repository on your machine!** if you do not do this your `notebook` folder on the Docker image will be empty. More detailed description of the image is available at the [Jupyter Notebook Data Science Stack Hub Page](https://hub.docker.com/r/jupyter/datascience-notebook/).
3. Run this command: `docker run -it -v PATH/:/home/jovyan/notebooks --rm -p 8888:8888 jupyter/datascience-notebook`
    * Quick explanation of the above command (don't worry if you don't follow this right now):
    * `-p 8888:8888` maps the 8888 port on the host OS to the 8888 port on the guest container. So if you were to go to http://localhost:8888, it will redirect to the 8888 port on the container - Jupyter Notebook starts a web server on that port on the guest.
    * `-v PATH/:/home/jovyan/notebooks` mounts the directory described by the `PATH` so that everything in that directory will be available in `notebooks` directory on the guest.  **Please check the hint above when you cloned the directory to find out what you need to change the PATH to!**
    * `jupyter/datascience-notebook` tells docker which image to pull from the Docker Hub. The first time you do this, it will take a few minutes (go grab a drink) to download everything it needs.  **Note that the download is several gigs so you will want to be on a fast, i.e., school, network if possible.**
4. Once everything is initialized and the notebook starts, you can connect it to by opening your web browser and going to: `http://localhost:8888/tree?token=279fb5e0fc0f240a90f913e7b9c9c068f36543a7d9544663`  --- the `token` will be different for you. Look for it in the output of the command above.

Some other trouble shooting notes for Docker:

* You can use the Docker GUI on Mac to start the notebooks as well - when you press run you'll need to enter in all the details for the container to make sure it works.
* You can configure VS Code to auto-launch notebooks in the Docker image above. This involves installing and following the directions for [Docker in Visual Studio Code](https://code.visualstudio.com/docs/containers/overview).
* If you are having trouble with the token you can try to start the notebook without a security token, however this is generally not recommended. Try the appending `start-notebook.sh --NotebookApp.token=''` to the above command.

**Note:** You can just install Anaconda or Python3 yourself and develop there if you wish.  However, you should ensure any code you run works on a Docker installation as described above. I will do all grading on the above Docker image and if your code doesn't run, then it's a 0.

## Python and Jupyter/IPython

We will be using Python for most of the assignments. Python is easy to pick up, and we will also provide skeleton code for most of the assignments. **IPython** is an enhanced command shell for Python, that offers enhanced introspection, rich media, additional shell syntax, tab completion, and rich history.

**Jupyter/IPython Notebook** started as a web browser-based interface to IPython, and proved especially popular with Data Scientists. A few years ago, the Notebook functionality was forked off as a separate project, called [Jupyter](http://jupyter.org/). Jupyter provides support for many other languages in addition to Python. Several other projects have been started in the recent years, inspired by the idea of Notebooks, e.g., Zeppelin.

Use the command listed above to start a docker container with Jupyter. On your local browser, go to: http://localhost:8888 (which requires you to enter the token).

* You should see the Notebooks in the `notebooks/` directory. Click to open the "Jupyter Getting Started" Notebook, and follow the instruction therein to make sure everything works!
* You should play with the Notebook to try out different Python commands. You can try creating a new notebook.

---

## Assignment

Follow the  `Project0` Notebook, and upload the `Project0.ipynb` file to Canvas. You can navigate to the [projects folder on GitHub if you want to see the file layout](https://github.com/nmattei/cmps6790/tree/main/_projects).

### Grading Rubric

* (5 Points) *Professionalism*: You have written code that is interpretable -- it contains comments where needed to understand, variable names are reasonable, and code that is reasonable and efficient. You have followed directions to turn in the file, clearly labeling everything. You have cited all sources and how you used them within the code or paper.
* (5 Points) *Visiting Office Hours*: You have visited office hours of at least one instructor of this course *before the assignment is due!*.
* (5 Points): *Docker Setup*: The project runs on the correct Docker image and the environment is setup correctly.
* (5 Points): *Function Correctness*: Function to count the letters is implemented and correct.  There are many right answers but we will take points if you do it extremely inefficiently.
* (5 Points): *Counters and Testing*: You have placed the correct amount of testing and demonstrated the max, min, and average functions. They are correct and implemented properly.

| Full    |    Good |  Okay |   Lacking   |   Poor  | No Marks |
| : ---- :| : ---- :| : ---- :| : ---- :| : ---- :| : ---- : |
| You completely and fully met the criteria described. | You have met most of the criteria but lack sufficient depth and/or missed one or more minor pieces. | You have missed components of the required criteria and/or they are incorrect / inappropriate or lack depth. | You have missed major components of the required criteria and/or may of them are incorrect. | Little to no evidence of work and major missing components. | Missing or completely inadequate. | 
