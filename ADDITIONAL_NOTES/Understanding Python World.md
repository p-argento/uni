Useful notes about
[[Python MAIN]]
[[Jupyter]]
[[NumPy]]
[[MatplotLib]]


*Jupyter* (formerly known as IPython Notebook) is an open-source code that combines Markdown text and executable Python source code in a notebook.
IPython means Interactive Computing with Python.

*Kernels* are programming language specific processes that run independently and interact with Jupyter Applications and their user interfaces. 
ipykernel is the reference Jupyter Kernel built on top of IPython, which enables using IPython as a kernel.

The default kernel for Jupyter is *IPython*, but also other kernels are available like R or Julia. The IPython kernel can be thought of as a reference implementation for Jupyter, as CPython is for Python.

Remember that *CPython* is the reference implementation of the Python Programming Language. Written in C and Python. It is basically the source code of Python.

*Pip* (or pip3) is a package-management system written in Python, used to install and manage software packages. It connects to an online repository of public packages, called the Python Package Index, or PyPI. (do not confuse PyPI with PyPy, an alternative implementation of Python).

*Conda* is an alternative to pip, is the package management tool for Anaconda. It allows for easy installation of different versions of python, libraries and tools into virtual environments. See also [[Understanding Conda]]. See also [[conda-cheatsheet.pdf]]

(from VSCode docs)
A *Python Environment* is a Python Interpreter (of a specific version) and an associated location for Python Packages). A Python Environment installed on a system can be used as a kernel to execute code.
The default kernel for Python is provided by the IPyKernel Package. If the environment selected does not have IPyKernel installed and you attempt to run the notebook, you will be prompted to install IPyKernel. If installed, the environment can be used as a valid kernel for jupyter notebook.
Note: You do not need install jupyter into the python environment. Only IPython and IPyKernel are required to launch a Python process as a kernel.
Remote Jupyter servers can be used, using their URLs.

Each Jupyter Kernel has a *Jupyter Kernel specification* (or Jupyter kernelspec), which contains a JSON file (kernel.json) with details about the kernel-name, description and CLI information required to launch a process as a kernel.
Basically, a kernel identifies itself to IPython by creating a directory, the name of which is used as an identifier for the kernel.
With my conda environment active, if I run `jupyter kernelspec list`, I get this file `/Users/pietro/anaconda3/share/jupyter/kernels/python3/kernel.json`
It contains ```
```json
{
 "argv": ["/Users/pietro/anaconda3/bin/python",  "-m",  "ipykernel_launcher",  "-f",  "{connection_file}" ],
 "display_name": "Python 3 (ipykernel)",
 "language": "python",
 "metadata": {  "debugger": false }
}
```

*PyTorch* is a deep learning framework used to build artificial intelligence software with Python. See [[Understanding PyTorch]]

*TensorFlow* is a tool for building deep neural networks with high-level Python code. It provides APIs to train, analyze and deploy ML models. See [[Understanding TensorFlow]]

*Pythonic* is referred to Python Style while Programming. See [[Organizing Python Code]]

