# Ansible Role: EPICS

[![main](https://github.com/lbl-camera/epics-ansible-role/actions/workflows/main.yml/badge.svg)](https://github.com/lbl-camera/epics-ansible-role/actions/workflows/main.yml)

This Ansible role installs the **EPICS Base**, selected EPICS **support** modules, **areadetector**, and areadetector **iocs** on **Debian** and **RedHat/CentOS**-based systems.

## Requirements

- Ansible 2.9+
- Git

## Example Playbook

This example playbook will the ADAndor IOC and all epics components required to support it.

```yaml
- name: epics
  hosts: all
  roles:
    - role: epics
      vars:
      areadetector_iocs:
        ADAndor: master
```

## Role Variables

### Location Variables
These variables should be defined in your playbook or inventory:

| Variable          | Description                                          | Default       |
|-------------------|------------------------------------------------------|---------------|
| `epics_dir`       | Directory to install EPICS                           | `/epics`      |
| `epics_version`   | EPICS Base version to install                        | `R7.0.8.1`    |
| `epics_host_arch` | Target architecture for EPICS (e.g., `linux-x86_64`) | Auto-detected |

### Support Modules

Support modules required for areadetector will be installed by default. You change the selection of which support 
modules to install, and their versions, by setting install_modules, for example:

```yaml
install_modules:
  asyn: "R4-44"
```

Support modules are installed in the order specified. This is important, as there are cross-dependencies. See the
defaults in `defaults/main.yml` for a typical install sequence.

### Dependency Variables

| Variable    | Description                                                                            | Default |
|-------------|----------------------------------------------------------------------------------------|---------|
| `use_tirpc` | Uses libtirpc as a provider of RPC related symbols (recommended on newer environments) | `yes`   |
| `use_xml2`  | Uses libxml2 as a provider of xml related symbols (recommended on newer environments)  | `yes`   |

### IOC Variables

By default, no areadetector IOCs will be installed. You must specify desired iocs (and versions) in the 
`areadetector_iocs` variable.

```yaml
areadetector_iocs:
  ADAndor: master
```

## For Developers
To accelerate local development of this role, you may use [act](https://github.com/nektos/act) to run the test workflow locally in an
isolated docker container. The steps for this are:

- Install Docker Desktop
- Download [act](https://github.com/nektos/act) and extract into this project directory
- Run `./act`
- (First run only) Select the "Medium" image as the default

Act then execute the workflow in an isolated environment, running the playbook at `.github/playbooks/test-playbook.yaml`.

---
This repo was forked from [infn-epics/epics-ansible-role](https://baltig.infn.it/infn-epics/epics-ansible-role/-/tree/main),
which provides a role for installing epics base and certain support IOCs. This repo is an extension and refactoring of
that to support areadetector and IOC installation.
