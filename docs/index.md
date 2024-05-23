# Homepage

For full documentation visit [mkdocs.org](https://www.mkdocs.org).

## Code Annotations Examples

### Codeblocks
some `code` goes here.

### Plain code block

A plain code block:

```py title="function for creating file paths" linenums="1"
import argparse
import getpass
import json
import logging
import os
import re
import sys
import timeit
from datetime import datetime

from icecream import ic
from netmiko import ConnectHandler
from netmiko.exceptions import AuthenticationException, NetmikoTimeoutException
from paramiko.ssh_exception import SSHException
```

```py title="function for removing blank lines" hl_lines="13-16"
def create_filename(sub_dir1: str, extension: str = "", sub_dir2="") -> str:
    """
    returns a valid path regardless of the OS

    Args:
        sub_dir1 (str): name of the sub directory off the cwd required
        extension (str, optional): string appended after hostname - ex. -interface.txt
        sub_dir2 (str, optional): if a nested sub_dir is used Defaults to "".

    Returns:
        str: full pathname of the file to be written
    """
    current_path = os.getcwd()
    extension = hostname + extension
    int_report = os.path.join(current_path, sub_dir1, sub_dir2, extension)
    return int_report


def remove_empty_lines(filename: str) -> str:
    """
    Removes empty lines from the file

    Args:
        filename (str): file in the cwd to be opened

    Returns:
        Nothing - updated file is written to disk
    """
    if not os.path.isfile(filename):
        print("{} does not exist ".format(filename))
        return
    with open(filename) as filehandle:
        lines = filehandle.readlines()

    with open(filename, "w") as filehandle:
        lines = filter(lambda x: x.strip(), lines)
        filehandle.writelines(lines)
```

## Project layout

    mkdocs.yml    # The configuration file.
    docs/
        index.md  # The documentation homepage.
        ...       # Other markdown pages, images and other files.

## Icons and Emojis

:smile:

:fontawesome-regular-face-laugh-wink:

:fontawesome-brands-twitter:{ .twitter }

:octicons-heart-fill-24:{ .heart }
