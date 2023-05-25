# pydpf-actions

This repository hosts github actions specific to DPF. Those actions ca be used in dpf dependent ci/cd
workflows for github.

## Hosted actions

### Action install-dpf-server
The action  named `install-dpf-server` is hosted in this repository.

#### Use the action
To use `install-dpf-server` in a github workflow, add this step:
```
- id: install-dpf
  uses: ansys/pydpf-actions/install-dpf-server@v2.3
  with:
    dpf-standalone-TOKEN: ${{secrets.DPF_PIPELINE}}
    ANSYS_VERSION : 232
```

#### Supported options
Linux and Windows hosted workflows are supported for ANSYS version 2022 R1.


### Action install-package
The action  named `install-package` is hosted in this repository.
It installs the package in the local repository.
It is used by the `build_package` and `build_doc` actions.

#### Use the action
To use `install-package` in a github workflow, add this step:
```
- name: "Install local package"
  uses: ansys/pydpf-actions/install-package@v2.3
```

#### Supported options
No option.


### Action build_package
The action  named `build_package` is hosted in this repository.
It installs and builds the local package, and then uploads the wheel as artifact.

#### Use the action
To use `build_package` in a github workflow, add this step:
```
- id: build_package
  uses: ansys/pydpf-actions/build_package@v2.3
  with:
    python-version: ********
    ANSYS_VERSION: ********
    PACKAGE_NAME: ********
    MODULE: ********
    dpf-standalone-TOKEN: ********
    install_extras: ********
```

#### Supported options
"python-version" can be any Python version as a string.
"ANSYS_VERSION" can be any version supported by pydpf-actions/install-dpf-server.
"PACKAGE_NAME" is used to name wheels and artifacts.
"MODULE" is used to specify the package module to test "import" and retrieve package version.
"dpf-standalone-TOKEN" is the token required by pydpf-actions/install-dpf-server.
"install_extras" is an optional list of extra requirements to be installed for this package.


### Action test_package
The action  named `test_package` is hosted in this repository.
It runs pytest on docstrings and on the tests for the installed local package and then
uploads the test results as artifacts.

#### Use the action
To use `test_package` in a github workflow, add this step:
```
- id: test_package
  uses: ansys/pydpf-actions/test_package@v2.3
  with:
    MODULE: ********
```

#### Supported options
"MODULE" is used to specify the package module to test.


### Action release_package
The action  named `release_package` is hosted in this repository.
It publishes the local DPF package to PyPi along with chosen artifacts.
Currently all present ".whl", ".tar.gz", ".pdf" and ".zip" artifacts 
are released.

#### Use the action
To use `release_package` in a github workflow, add this step:
```
- name: Release Package
  uses: ansys/pydpf-actions/release_package@v2.3
  with:
    PYPI_TOKEN: ${{ secrets.PYPI_TOKEN }}
```

#### Supported options
"PYPI_TOKEN" is the token for publishing on PyPi.


### Action build_doc
The action  named `build_doc` is hosted in this repository.
It generates the html and pdf documentation using sphinx for the local DPF package.
It then zips it and uploads it as artifact.

#### Use the action
To use `build_doc` in a github workflow, add this step:
```
- id: build_doc
  uses: ansys/pydpf-actions/build_doc@v2.3
  with:
    python-version: "3.8"
    ANSYS_VERSION: 232
    PACKAGE_NAME: ansys-dpf-post
    MODULE: post
    dpf-standalone-TOKEN: ${{secrets.DPF_PIPELINE}}
    install_extras: plotting
  timeout-minutes: 30
```

#### Supported options
"python-version" can be any Python version as a string.
"ANSYS_VERSION" can be any version supported by pydpf-actions/install-dpf-server.
"PACKAGE_NAME" is used to name wheels and artifacts.
"MODULE" is used to specify the package module to test "import" and retrieve package version.
"dpf-standalone-TOKEN" is the token required by pydpf-actions/install-dpf-server.
"install_extras" is an optional list of extra requirements to be installed for this package.
A timeout is advised to prevent the pipeline from getting stuck.


### Action push_doc
The action  named `push_doc` is hosted in this repository.
It pushes the previously generated documentation to the release branch and the ansys "DOC-REPO".

#### Use the action
To use `push_doc` in a github workflow, add this step:
```
- name: "Push Documentation"
  uses: ansys/pydpf-actions/push_doc@v2.3
  with:
    PYANSYS_CI_BOT_TOKEN: ${{secrets.PYANSYS_CI_BOT_TOKEN}}
    DOC_REPO: DPF-Post-docs
```

#### Supported options
"PYANSYS_CI_BOT_TOKEN" is the token required to commit on the ansys repo.
"DOC_REPO" is the name of the ansys documentation repository to update.


### Action kill-dpf-servers
The action  named `kill-dpf-servers` is hosted in this repository.
It kills all DPF servers currently running.
It is used by the `build_package`, `test_package` and `build_doc` actions.

#### Use the action
To use `kill-dpf-servers` in a github workflow, add this step:
```
- name: "Kill all servers"
  uses: ansys/pydpf-actions/kill-dpf-servers@v2.3
```

#### Supported options
No option.


### Action check-licenses
The action  named `check-licenses` is hosted in this repository.
It checks licenses of all installed packages in the current environment.
It is used by the `build_package` action.

#### Use the action
To use `check-licenses` in a github workflow, add this step:
```
- name: "Check licences of packages"
  uses: ansys/pydpf-actions/check-licenses@v2.3
```

#### Supported options
No option.


## Testing

Ci/cd is implemented to test and showcase some actions on linux and windows.
