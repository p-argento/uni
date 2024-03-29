# Jupyter best practices
Jupyter best practices from [google](https://cloud.google.com/blog/products/ai-machine-learning/best-practices-that-can-improve-the-life-of-any-developer-using-jupyter-notebooks)
Should watch this [video](https://www.youtube.com/watch?v=xU_xdogXFeE&t=2545s)

Key points
1. institute version control
2. parameterized notebook?

**Follow established software development best practices**

This is essential. Jupyter Notebook is just a new development environment for writing code. All the best practices of software development should still apply:
- Version control and code review systems (e.g. git, mercurial).
- Separate environments: split production and development artifacts.
- A comprehensive test suite (e.g. unitests, doctests) for your Jupyter Notebooks.
- Continuous integration (CI) for faster development: automate the compilation and testing of Jupyter notebooks every time a team member commits changes to version control.
Just as an Android Developer would need to follow the above best practices to build a scalable and successful mobile app, a Jupyter Notebook focused on sustainable data science should follow them, too.

## Version control
To apply the principles and corresponding workflows of traditional version control to Jupyter notebooks, you need the help of two additional tools:
- [`nbdime`](https://github.com/jupyter/nbdime): tool for “diffing” and merging of Jupyter Notebooks
- [`jupyterlab-git`](https://github.com/jupyterlab/jupyterlab-git): a JupyterLab extension for version control using git

## Reproducible notebooks
You and your team should write notebooks in such a way that anyone can rerun it on the same inputs, and produce the same outputs. Your notebook should be executable from top to bottom and should contain the information required to set up the correct, consistent environment.
It means that
- All dependencies should be installed by the notebook itself.
- A notebook should be executable from top to bottom without any errors.
Exactly like RProjects.

This might be interesting https://github.com/nteract/papermill
## Continuous integration
Continuous integration is a software development practice that requires developers to integrate code into a shared repository. Each check-in is verified by an automated build system, allowing teams to detect problems at early stages. Each change to a Jupyter notebook should be validated by a continuous integration system before being checked in; this can be done using different setups (non-master remote branch, remote execution in local branch, etc)