# What is Conda
Note that Conda is the package manager, while Anaconda and Miniconda are distributions. A package manager is a tool that automates the process of installing, updating and removing packages. A software distribution is a collection of packages, pre-built and pre-configured, that can be installed and used on a system.

> Anaconda is a full distribution of the central software in the PyData ecosystem, and includes Python itself along with the binaries for several hundred third-party open-source projects. Miniconda is essentially an installer for an empty conda environment, containing only Conda, its dependencies, and Python.

Run `conda list` to see all packages installed. And note that python is there, as well as jupyter, ipython and ipykernel.
See other commands in the [[conda-cheatsheet.pdf]]
Note that
- You can abbreviate many frequently used command options that are preceded by 2 dashes (`--`) to just 1 dash and the first letter of the option. So `--name` and `--envs` can be written as `-n` and `-e` respectively.

# Virtual Environments

source: [https://www.youtube.com/watch?v=qI3P7zMMsgY]

It is possible to have multiple versions of python.
They are managed using Virtual Environments.
The best way to do it is using Anaconda.
All the following code is for the mac terminal.

There is a built-in version of Python on the mac.
More versions can be installed.
In particular, they can be installed in virtual environment.
`conda` to check if Anaconda is installed.
To create a new virtual environment use:
```terminal
conda create --name <env_name> python=3.11
conda activate <env_name>
...
conda deactivate
```
If packages are installed when using a virtual env, then it is installed only for that specific version of python.
To see all the environments created use
`conda info --envs`
And to remove (-n stands for -name)
`conda env remove -n <env_name>`


