Virtual environments are highly suggested way to compartmentalize your Python projects from each other. Effectively a virtual environment is a distinct copy of the Python runtime that you can install your project's requirements to without affecting the system-wide Python or other projects you might have.

Take, for example, two projects you might have:
```
Project Foo
Requirements:
	numpy~=1.20.1
	torch~=1.3.0

Project Bar
Requirements:
	numpy~=2.1.0
	torch~=2.4.0
```
Note how both projects have different version requirements for `numpy` and `torch`. While the given packages are quite good at having solid [backward compatibility](https://en.wikipedia.org/wiki/Backward_compatibility), there will inevitably be some changes between the versions that might not be compatible with the given projects' use of the packages. Simply running `pip install -r requirements.txt` for both projects will inevitably break either one (or both!) of the projects. 

Python, [since v3.3](https://peps.python.org/pep-0405/), is commonly packaged with the `venv` package. As the name might suggest, this package deals with creating virtual environments. It's use is quite simple, though not without some things to keep in mind. In it's most basic form, you can run
```shell
python -m venv .venv
```
to create a new virtual environment in the directory `.venv` of the directory where your shell currently is active. You're not yet using the new virtual environment though! First, you have to activate the new environment in your [[CLI|shell]] with
```shell
# Windows CMD
cd .venv/Scripts
activate
cd ../..

# Windows Powershell
./.venv/Scripts/activate

# MacOS Zsh and Linux Sh/Bash
source .venv/bin/activate
```

When successful, you should see something like `(.venv)` in front of your shell input:
```shell
# Linux
(.venv) ~$ 

# Windows Powershell
(.venv) PS C:\
```
Now you're ready to start installing your project's requirements!

## Other solutions
While `venv` is bundled with Python, other external solutions exist. One popular one is [Conda](https://github.com/conda/conda), on which [Anaconda](https://www.anaconda.com/) is built. One benefit of Conda is that it also provides pre-built binaries for packages and libraries that are commonly used in scientific settings. As a whole, it serves the same function as `pip` and `venv` in one package, with the drawback that it tends to be quite heavyweight for anything but the most intricate projects. Furthermore, at time of writing, it doesn't play well with Python's [[Project Requirements|recently introduced method]] of declaring project requirements.

