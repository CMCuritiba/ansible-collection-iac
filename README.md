# Ansible Collection - CMCuritiba.IaC

Documentation for the collection.

This is still a work in progress.

Requirements:

- Ansible 2.10.3 or higher
- Python 3.8.5 or higher

Instructions for installing CMCuritiba.IaC:

- Optional: Create a python virtual environment and activate it before executing subsequent steps.

  1. Install the following packages (use the latest available version):
     1. Ansible
  1. Install collection using ansible galaxy (**TODO**):
     1. Example command to install:
        `ansible-galaxy collection install CMCuritiba.IaC`
     1. Example command to upgrade to the latest version:
          `ansible-galaxy collection install CMCuritiba.IaC --force`
  1. Update existing playbooks to work with collection:
     1. Rename all roles referenced inside playbooks to begin with CMCuritiba.IaC.
     1. Remove all references to `cmc_server_hostname`. `cmc_server_hostname` was replaced with ansible's `inventory_hostname_short` special variable.
  1. Miscellaneous
     1. Please submit a pull request on so we can merge your roles into the collection.
