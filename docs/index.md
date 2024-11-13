# Homepage

For full documentation visit [mkdocs.org](https://www.mkdocs.org).

Video explaining how to use github pages: [Youtube](https://www.youtube.com/watch?v=Q-YA_dA8C20)

Video covering Admonitions and other features: [Material for MkDocs: Full Tutorial To Build And Deploy Your Docs Portal](https://www.youtube.com/watch?v=xlABhbnNrfI) 

## Code Blocks

[Code blocks](https://squidfunk.github.io/mkdocs-material/reference/code-blocks/) and examples are an essential part of technical project documentation. Material for MkDocs provides different ways to set up syntax highlighting for code blocks, either during build time using Pygments or during runtime using a JavaScript syntax highlighter.

## Code Annotations Examples

### Codeblocks

some `code` goes here.

### Plain code block

A plain code block:

```py title="imports" linenums="1"
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

```py title="function for creating file paths" linenums="1"
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
```

```py title="function for removing blank lines" hl_lines="11-13"
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

## Project Directory Layout

    mkdocs.yml    # The configuration file.
    docs/
        index.md  # The documentation homepage.
        ...       # Additional markdown pages, and other files.
        img/      # Images

## Icons and Emojis

https://squidfunk.github.io/mkdocs-material/reference/icons-emojis/#search

This configuration enables the use of icons and emojis by using simple shortcodes which can be discovered through the icon search. Add the following lines to mkdocs.yml:

```yml
markdown_extensions:
  - attr_list
  - pymdownx.emoji:
      emoji_index: !!python/name:material.extensions.emoji.twemoji
      emoji_generator: !!python/name:material.extensions.emoji.to_svg
```



### Using emojis
Emojis can be integrated in Markdown by putting the shortcode of the emoji between two colons. If you're using [Twemoji](https://github.com/twitter/twemoji) (recommended), you can look up the shortcodes at [Emojipedia](https://emojipedia.org/twitter/):

``` title="Emoji"
:smile:
```

:smile:

:fontawesome-regular-face-laugh-wink:

:fontawesome-brands-twitter:{ .twitter }

:octicons-heart-fill-24:{ .heart }

## Admonitions

[Admonitions](https://squidfunk.github.io/mkdocs-material/reference/admonitions/), also known as call-outs, are an excellent choice for including side content without significantly interrupting the document flow. Material for MkDocs provides several different types of admonitions and allows for the inclusion and nesting of arbitrary content.

Each of the supported admonition types has a distinct icon, which can be changed to any icon bundled with the theme, or even a [custom icon](https://squidfunk.github.io/mkdocs-material/setup/changing-the-logo-and-icons/#additional-icons). Add the following lines to mkdocs.yml:

```
theme:
  icon:
    admonition:
      <type>: <icon>
```

Alternate Icons Github

```
theme:
  icon:
    admonition:
      note: octicons/tag-16
      abstract: octicons/checklist-16
      info: octicons/info-16
      tip: octicons/squirrel-16
      success: octicons/check-16
      question: octicons/question-16
      warning: octicons/alert-16
      failure: octicons/x-circle-16
      danger: octicons/zap-16
      bug: octicons/bug-16
      example: octicons/beaker-16
      quote: octicons/quote-16
```

Alternate Icons Fontawesome

```
theme:
  icon:
    admonition:
      note: fontawesome/solid/note-sticky
      abstract: fontawesome/solid/book
      info: fontawesome/solid/circle-info
      tip: fontawesome/solid/bullhorn
      success: fontawesome/solid/check
      question: fontawesome/solid/circle-question
      warning: fontawesome/solid/triangle-exclamation
      failure: fontawesome/solid/bomb
      danger: fontawesome/solid/skull
      bug: fontawesome/solid/robot
      example: fontawesome/solid/flask
      quote: fontawesome/solid/quote-left
```

### Usage
Admonitions follow a simple syntax: a block starts with !!!, followed by a single keyword used as a type qualifier. The content of the block follows on the next line, indented by four spaces:

``` title="Admontion"
!!! note

    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod
    nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor
    massa, nec semper lorem quam in massa.
```

### Changing the title
By default, the title will equal the type qualifier in titlecase. However, it can be changed by adding a quoted string containing valid Markdown (including links, formatting, ...) after the type qualifier:

``` title="Admonition with a title
!!! note "Phasellus posuere in sem ut cursus"

    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod
    nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor
    massa, nec semper lorem quam in massa.
```

Removing the title
Similar to [changing the title](https://squidfunk.github.io/mkdocs-material/reference/admonitions/#changing-the-title), the icon and title can be omitted entirely by adding an empty string directly after the type qualifier. Note that this will not work for [collapsible blocks](https://squidfunk.github.io/mkdocs-material/reference/admonitions/#collapsible-blocks):

```
!!! note ""

    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod
    nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor
    massa, nec semper lorem quam in massa.
```

### Collapsible blocks
When [Details](https://squidfunk.github.io/mkdocs-material/setup/extensions/python-markdown-extensions/#details) is enabled and an admonition block is started with ??? instead of !!!, the admonition is rendered as a collapsible block with a small toggle on the right side:

``` title="Admonition, collapsible"
??? note

    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod
    nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor
    massa, nec semper lorem quam in massa.
```

Adding a + after the ??? token renders the block expanded:

``` title="Admonition, collapsible and initially expanded"
???+ note

    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod
    nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor
    massa, nec semper lorem quam in massa.
```

### Inline blocks
Admonitions can also be rendered as inline blocks (e.g., for sidebars), placing them to the right using the inline + end modifiers, or to the left using only the inline modifier:

``` title="Inline End"
!!! info inline end "Lorem ipsum"

    Lorem ipsum dolor sit amet, consectetur
    adipiscing elit. Nulla et euismod nulla.
    Curabitur feugiat, tortor non consequat
    finibus, justo purus auctor massa, nec
    semper lorem quam in massa.
```


``` title="Inline"
!!! info inline "Lorem ipsum"

    Lorem ipsum dolor sit amet, consectetur
    adipiscing elit. Nulla et euismod nulla.
    Curabitur feugiat, tortor non consequat
    finibus, justo purus auctor massa, nec
    semper lorem quam in massa.
```


Important: admonitions that use the `inline` modifiers must be declared prior to the content block you want to place them beside. If there's insufficient space to render the admonition next to the block, the admonition will stretch to the full width of the viewport, e.g., on mobile viewports.

## Supported types
Following is a list of type qualifiers provided by Material for MkDocs, whereas the default type, and thus fallback for unknown type qualifiers, is `note`:

note
!!! note
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor massa, nec semper lorem quam in massa


abstract
!!! abstract
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor massa, nec semper lorem quam in massa.


info
!!! info
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor massa, nec semper lorem quam in massa.


tip
!!! tip
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor massa, nec semper lorem quam in massa.


success
!!! success
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor massa, nec semper lorem quam in massa.


question
!!! question
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor massa, nec semper lorem quam in massa.


warning
!!! warning
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor massa, nec semper lorem quam in massa.


failure
!!! failure
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor massa, nec semper lorem quam in massa.


danger
!!! danger
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor massa, nec semper lorem quam in massa.


bug
!!! bug
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor massa, nec semper lorem quam in massa.


example
!!! expample
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor massa, nec semper lorem quam in massa.


quote
!!! quote
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor massa, nec semper lorem quam in massa.



### Admonition icons


