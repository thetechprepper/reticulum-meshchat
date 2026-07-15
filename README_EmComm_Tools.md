# MeshChat for EmComm Tools

The following are my personal notes on building a modified version of
MeshChat. My build is specifically intended to produce a version suitable
for EmComm Tools and reflects the requirements and constraints of that
project.


## Features

* Fullscreen toggle for NomadNet Pages
* Bumped Reticulum version to 1.3.5


## Prerequisites

MeshChat requires:

* Node.js 18 or later
* Python 3.x

Verify your installed versions:

```bash
node --version
```

Example output:

```text
v22.14.0
```

Verify Python:

```bash
python3 --version
```

Example output:

```text
Python 3.10.7
```

## Building the Project

### 1. Install Node.js Dependencies

```bash
npm install
```

### 2. Install Python Dependencies

```bash
python3 -m pip install -r requirements.txt
```

### 3. Build the Front-End

```bash
npm run build-frontend
```

## Building the Electron Application

MeshChat can be packaged as a standalone Electron application for
Linux, macOS, and Windows.

### 1. Install Electron Build Dependencies

MeshChat uses `cx_Freeze` to package the Python backend.

```bash
python3 -m pip install --upgrade cx_Freeze
```

Verify that `cx_Freeze` is installed:

```bash
python3 -c "import cx_Freeze"
```

If no output is displayed, the package was installed successfully.

### 2. Build the Electron Application

From the root of the MeshChat source tree, run:

```bash
npm run dist
```

The build process will:

* Build the Electron front-end
* Build the Python backend using `cx_Freeze`
* Generate distributable packages using Electron Builder

The resulting installation packages will be placed in the `dist`
directory.
