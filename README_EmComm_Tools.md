# MeshChat for EmComm Tools

The following are my personal notes on building a modified version of
MeshChat. My build is specifically intended to produce a version suitable
for EmComm Tools and reflects the requirements and constraints of that
project.


## Features

* Fullscreen toggle for NomadNet Pages
* Bumped Reticulum version to 1.3.8
* Paper message creation and ingestion


## Prerequisites

MeshChat requires:

* Node.js 18 or later
* Python 3.x


## Building the Project

1. Install Node.js dependencies.

```bash
npm install
```

2. Install Python dependencies.

```bash
python3 -m pip install -r requirements.txt
```

3. Build the front-end.

```bash
npm run build-frontend
```


## Building the Electron Application

1. Install Electron build dependencies. MeshChat uses `cx_Freeze` to
   package the Python backend.

```bash
python3 -m pip install --upgrade cx_Freeze
```

2. Build the Electron application.

```bash
npm run dist
```
