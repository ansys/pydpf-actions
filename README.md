# pydpf-actions

This repository hosts github actions specific to DPF. Those actions ca be used in dpf dependent ci/cd
workflows for github.

## Hosted actions

### Action install-dpf-server
The action  names `install-dpf-server` is hosted in this repository.

#### Use the action

To use `install-dpf-server` in a github workflow, add this step:
```
- id: install-dpf
  uses: pyansys/pydpf-actions/install-dpf-server@v1
  with:
    dpf-standalone-TOKEN: ${{secrets.DPF_PIPELINE}}
    ANSYS_VERSION : 221
```

#### Supported options

Linux and Windows hosted workflows are supported for ANSYS version 2022 R1.

## Testing

Ci/cd is implemented to test the actions on linux and windows.