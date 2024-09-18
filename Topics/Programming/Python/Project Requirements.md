Historically, Python project requirements were frequently defined in the venerable `requirements.txt`. This is a simple text file that listed each installed package with version on each line. Any users of your project could install (hopefully) the same exact packages by running
```shell
pip install -r requirements.txt
```
This method was (and is) quite popular because it was fairly low effort to create a `requirements.txt` file with the following:
```shell
pip freeze > requirements.txt
```

An example of `requirements.txt` could look something like this:
```text
numpy==1.21.1
torch==1.3.0
scipy==1.0
```

Problems arise when any of the package versions are pulled from PyPi, or when the Python version you're trying to use is not supported by the packages. This has a larger chance of happening when the project you're trying to use is on the older side.

## `pyproject.toml`
Fairly recently, Python Enhancement Proposals (PEP) [518](https://peps.python.org/pep-0518/) and [621](https://peps.python.org/pep-0621/) have introduced and stabilized the `pyproject.toml` format as the new preferred method to define your project's metadata and dependencies. An added benefit that the specification has is that it is expected to serve as the universal specification for a wide range of build methods to use when managing the project. This should cut down on each distinct package manager having their own special format that is not interchangeable.

The `pyproject.toml` file lives at the root of your project, the same place where you'd generally find the `requirements.txt`, and specifies some information that build systems need to properly install your project dependencies. As specified in PEP 621, the following is a minimal example of a `pyproject.toml`:
```toml
[project]
name = "myproject"
```
That's it! All the specification really requires is the name of your project. But we do probably want to specify a few more things:
```toml
[project]
name = "myproject"
version = "0.1.0"
requires-python = ">=3.12"
authors = [
	{name = "Lois Lane", email = "l.lane@dailyplanet.com"}
	{name = "Clark Kent"}
]
maintainers = [
	{name = "Lex Luthor", email = "bossman@lexcorp.com"}
]
dependencies = [
	"matplotlib ~= 3.9.2"
	"numpy ~= 2.1.1",
	"requests ~= 2.23.3",
]

[project.optional-dependencies]
test = [
	"pytest",
]

[build-system]  
requires = ["setuptools"]  
build-backend = "setuptools.build_meta"
```

## Explanation
The above `pyproject.toml` has a few more things than the minimal example, we'll go through them
### Version
The version field in the file specifies the [semantic version](https://semver.org/) of your project. This string **must** follow pep [440](https://peps.python.org/pep-0440/), which reads like it is a lot scarier than it really is. The basic form of semantic versioning is that the first number is the **major** version, which would specify that a major change has occurred that most likely is not backwards compatible with the previous major version. The second number tends to be seen as the **minor** version. A minor update can introduce a new feature and change some fairly small things that *may* not always be backwards compatible. The third number tends to be a bugfix update. These tend to not be breaking changes (unless you were somehow relying on the bug!).

>[!info]
>Semantic versioning does not actually have any rules to it, but the `M.m.b` format is the most common one. Other formats include a date-based versioning system, such as `2024.9`. Read the [PEP 440 page](https://peps.python.org/pep-0440/) for more a in-depth explanation.

### Authors/Maintainers
As the names of suggest, these specify who initially made the project, and if someone has now taken over development, who maintains the project. The entries can contain a name, and an email address, and must be specified on the same line per person. Note that the exact definition of Author/Maintainer is up to the project owners.

### Requires-Python
The `requires-python` field specifies which versions of Python are valid for your project. If, for example, you want to use [[Type Hints]], you'd need at least version 3.5, so you'd write
```toml
requires-python = ">=3.5"
```
If one of your dependencies doesn't work with Python 3.9 and above, you can change the line to
```toml
requires-python = ">=3.5, <3.9"
```
If someone tries to install your project while they're using a Python version that is not supported, the installer will error out.

### Dependencies/Optional-Dependencies
These are the real meat of your requirements specification. The basic `dependencies` entry is defined in the PEP as being a list of strings, following PEP [508](https://peps.python.org/pep-0508/) and [440](https://peps.python.org/pep-0440/). PEP 508 describes how you should format a string to serve as a correct package name and version specifier, and 440 additionally describes [how you may use comparators](https://packaging.python.org/en/latest/specifications/version-specifiers/#version-matching) for version range selection. In short, there are a few things you can do:
```toml
dependencies = [
	"no-version",
	"minimum-version >= 1.0",
	"between-versions >= 1.0, <2.0",
	"only-this-version == 1.0",
	"except-this-version >1.0, != 1.1",
	"compatible-version ~= 1.0.0"
]
```

>[!note]
>The `compatible-version` specifies it's version with the `~=` operator. This indicates that it will match with any version `>= 1.0.0, <1.1.*`. The granularity of compatibility is determined by how many steps into the version scheme you define it. If we had written
>`compatible-version ~= 1.0`
>We'd have matched with any version `>=1.0, <2.0`. See the [Compatible Release section](https://packaging.python.org/en/latest/specifications/version-specifiers/#compatible-release)

Optional-dependencies work similar, but are split off from the main `[project]` table to allow for the following syntax:
```toml
[project.optonal-dependencies]
all = [
	"myproject[dev,jupyter]"
]
dev = [
	"black",
	"isort",
	"pytest"
]
jupyter = [
	"jupyterlab"
]
```
where each field creates a new extra that you can optionally install. For example, if the user wants to use `jupyter` functionality in your project, they could run
```shell
pip install myproject[jupyter]
```
to select the required optional dependencies. Finally, you can also specify a combination of your extras by using the name of your project, together with the extras you want to bundle together.

### Build-System
Last but not least, the `build-system` table specifies which build system you want to use for your project. The most common one that is used for pure python systems is `setuptools`. To specify this, we set `requires = ["setuptools"]`, but if your project has any other requirements that you may need during a `pip install`, you can add them to this list. These packages will **only** be installed during the build, so any package that you also need during runtime should also be specified under `dependencies`.

The `build-backend` field specifies which of the packages in `reduires` we should use, and which command from that package we should build with.

# Installing your project
If you have a need to install your project, for example as a package for another project, but have not published it to PyPi, you can simply install it using
```shell
pip install /path/to/project
```
where the path to the project should be the directory where your `pyproject.toml` file is located.

An option you can pass as well is the editable flag, `-e` or `--editable` like so:
```shell
pip install -e /path/to/project
```
which lets you edit the files in your project to quickly fix bugs or add features as needed without having to reinstall the entire package.