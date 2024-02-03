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


