# OSX Packages Uninstaller

This software is aimed to help manage packages uninstalling in OSX.

## Installation

Installation is as simple as:

    [sudo] bash < <(curl -sL https://raw.github.com/mpapis/pkg_uninstaller/master/pkg-install)

Adding to PATH, for system installation (with sudo):

    echo 'PATH=$PATH:/opt/pkg_uninstaller' >> /etc/profile
    
Adding PATH when installed as user (without sudo):

    echo 'PATH=$PATH:$HOME/.pkg_uninstaller' >> $HOME/.bash_profile

Note the single quotes are important in both cases.

## Installing package file

Install packages with:

    pkg-install <package_file.pkg>

This will create `uninstall_<package_file_pkg>.sh` in current directory.

To uninstall this package just execute `./uninstall_<package_file_pkg>.sh`.

### Example

    # coming soon

## Uninstalling single packages by name.

List available package names (possibly filtering by [name]):

    pkg-list [name]

Uninstall package:

    pkg-uninstall <name>

## Using internally in package to build uninstaller

1. You have to bundle `pkg-wrapper` with your application 
and install it to disk before executing the hook bellow.

1. In before installing hook call this script:

    #!/bin/bash
    
    pkg-wrapper before "your package name"

1. In after installing hook call this script:

    #!/bin/bash
    
    pkg-wrapper before "your package name" /path/to/uninstaller_name.sh

1. In uninstall hook call:

    #!/bin/bash
    
    /path/to/uninstaller_name.sh
    rm /path/to/uninstaller_name.sh
