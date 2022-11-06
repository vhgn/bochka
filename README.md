# Description

Bochka is a simple package manager for C that I needed so much.
It uses line based [config files](#structure) of GitHub repository names for dependencies.

> Just a side-project, not ready for any serious use

# Installation

- Clone this repository
- Run `make` in it (to build the binary)
- Run `make install` to install globally

# Usage

## Binaries

Create a `Bochkadeps` file and put dependencies there (see [structure](#structure)).

Use `bochka` command to fetch all packages in `/pkg`, build them, put static library files in `/lib`.

> You can use _bochka_ `def/Makefile` for quick defaults

## Packages

Create a `Bochkapkg` file with a single line containing the name of a package
Also, create a `Makefile` which generates a static library with the name `libname.a`, where the name is the same as in `Bochkapkg`.

These are the only requirements for a package, possibilities are limitless.

# Structure

`Bochkapkg` file has a single line with the name of the project in it (used as a static library name).
`Bochkadeps` file has each dependency on **a new line**.
It uses Git repository URL of existing _bochka_ projects (which will be used with `git clone`).

```
https://example.com/user/repo
https://example.com/other/lib
```

---

A _bochka_ project **must** have flat source file structure like this:

- Source files, named `*.c` (no tests are allowed yet, see [coming](#coming) section)
- Header files, named `*.h` (they will be included like: `#include "pkg/user/repo/file.h"`)

---

A typical _bochka_ project may look like this:

```
.
|-- .gitignore
|-- Bochkadeps
|-- Bochkapkg
|-- LICENSE
|-- Makefile
|-- README.md
|-- name.c
|-- name.h
|-- other.c
|-- other.h
```

> Object files (`name.o`, `other.o`) and a static library (`libname.a`, assuming the content of `Bochkapkg` is just `name`) are compiled from the sources.

# Logic

When you run `bochka` in a project:

- Fetches dependencies of a package
- Builds object files inside their directory
- Creates a static linked library and puts inside your `/lib` directory

# Contribution

I use [conventional commits](https://www.conventionalcommits.org/en/v1.0.0/) for structured commit messages.

> Feel free to open issues for bugs and new features, or create a pull request

# Coming

- Fetching the dependencies in a global directory to avoid redundant fetch calls
- Fetching, building and installing binary executables
