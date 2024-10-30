# Ansible Role: EPICS

This Ansible role installs the **EPICS Base** and selected EPICS modules, such as **asyn**, **modbus**, **streamdevice**, **motor**, **devLib2**, **autosave**, **calc**, and **busy**, on **Debian** and **RedHat/CentOS**-based systems.

## Requirements

- Ansible 2.9+
- Git
- Required development tools and libraries (installed by the role)

## Role Variables

### Required Variables
These variables should be defined in your playbook or inventory:

| Variable            | Description                                                   | Default          |
|---------------------|---------------------------------------------------------------|------------------|
| `epics_base_dir`    | Directory to install EPICS Base                               | `/opt/epics/base` |
| `epics_version`     | EPICS Base version to install                                 | `7.0.5`           |
| `epics_modules_dir` | Directory to install EPICS modules                            | `/opt/epics/modules` |
| `epics_host_arch`   | Target architecture for EPICS (e.g., `linux-x86_64`)          | Auto-detected    |

### Optional Module Variables
These modules can be included and configured as needed. Set the relevant variable to `yes` to enable installation.

| Variable                  | Description                            | Default   |
|---------------------------|----------------------------------------|-----------|
| `install_asyn`            | Install asyn module                   | `no`      |
| `install_modbus`          | Install modbus module                 | `no`      |
| `install_streamdevice`    | Install streamdevice module           | `no`      |
| `install_motor`           | Install motor module                  | `no`      |
| `install_devlib2`         | Install devLib2 module                | `yes`     |
| `install_autosave`        | Install autosave module               | `no`      |
| `install_calc`            | Install calc module                   | `no`      |
| `install_busy`            | Install busy module                   | `no`      |

Each module's version can be specified using `module_name_version` (e.g., `asyn_version`).

## Dependencies

None.

## Example Playbook

```yaml
- hosts: all
  roles:
    - role: epics
      vars:
        epics_base_dir: "/opt/epics/base"
        epics_version: "7.0.5"
        install_asyn: yes
        install_modbus: yes
        install_streamdevice: yes
        install_motor: yes
        install_autosave: yes
        install_calc: yes
        install_busy: yes
```