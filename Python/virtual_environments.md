# Sources
1. Articles - [Main (from RealPython)](https://realpython.com/python-virtual-environments-a-primer/)

# Summary

### Quick Start


This assumes you are using Python 3, the PowerShell and the venv module from the standard library.

#### Create folder to store the virtual environment:

    $ mkdir python-virtual-environments
    $ cd python-virtual-environments

#### Create the virtual environment:

    $ python -m venv env

This generates the following folders:

- Include - C headers that compile the Python packages
- Lib - a copy of the Python version along with a site-packages folder where each dependency is installed
- Scripts - files that interact with the virtual environment

#### Activate the environment

> The activate scripts are used to set up your shell to use the environment’s Python executable and its site-packages by default.

    $ env/Scripts/activate

In my particular case I had to change PS's execution policy:

    $ Set-ExecutionPolicy RemoteSigned -Scope CurrentUser

>Notice how your prompt is now prefixed with the name of your environment (env, in our case). This is the indicator that env is currently active, which means the python executable will only use this environment’s packages and settings.

#### How to deactivate

    $ deactivate

Always do this when you're done with a specific virtual environment.

### How it actually works

Activating the venv changes the $PATH environment variable to look first into the location `python-virtual-environments\env\Scripts` for python.exe.

>There actually isn’t any difference between these two Python executables. It’s their directory locations that matter.

Different locations. Different site-packages folders are considered.

### Next Steps

Use virtualenvwrapper/virtualenvwrapper-win module to:
- Organize all of your virtual environments in one location
- Provide methods to help you easily create, delete, and copy environments
- Provide a single command to switch between environments

Use pyenv/pywin module to:
- Use different versions of Python as well



 


