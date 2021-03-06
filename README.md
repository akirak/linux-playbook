Ansible Playbooks for Configuring a Linux Desktop
==================

[![Build Status](https://travis-ci.org/akirak/linux-playbook.svg?branch=master)](https://travis-ci.org/akirak/linux-playbook)

This repository contains Ansible playbooks for configuring a Linux machine.

## Features

This repository consists of two playbooks: one for the root user and another for a normal user. 

### Playbook for the root

[The root playbook](init.yml) must be run as the root user in the very beginning of installation. Like cloud-init, it creates the default user for an operating system and optionally deploys X Window System. 

This playbook currently supports only Arch Linux, as most *desktop* operating systems ship with a graphical environment and force you to create at least one normal user. 

### Playbook for a user

Another playbook should be run as a user. It deploys the following programs and configuration files. 

- Zsh
- Environment variables for Emacs and Chrome
- Input methods for Japanese and Chinese
- Add multilib, archlinuxfr, and archlinuxcn repositories for Arch Linux pacman

In terms of playbook organization, it has made the following progress. 

- The entire playbook is rewritten. It is neatly organized using pre-tasks and roles. 
- Tags are added to each role so that you can select features you need. 
- A generic package module of Ansible is used to install common packages. Hopefully, it supports other Linux distributions out of the box. 
- For more specific packages such as utilities, tasks are conditionally run or just skipped in unsupported operating systems. 

## Supported platforms

This root playbook supports only Arch Linux.

The user playbook is currently tested on Arch Linux but may support other Linux distributions in the future. 

## Usage

### Create a user and deploy a graphical environment

This repository contains a script for creating a user and installing X Window System on Arch Linux:

    bash ./install.bash

or

    make install

If you don't want to install the graphical environment using this playbook, add `--skip-tags=x-server` option:

    bash ./install.bash --skip-tags=x-server

### Install applications as a user

    bash ./install.bash

or

    make install
    
## Development

To create a user and install applications (excluding X application) as the Linux onto Arch Linux:

    make archlinux

To install all applications onto Arch Linux:

    make archliux-full

## License

[MIT License](LICENSE)
