---
title: Command Line Interface (CLI)
description: Terramate has a rich command-line interface, supporting verbosity levels, logging levels, multiple sub-commands, autocompletion and more.

prev:
  text: 'Upgrade Check'
  link: '/configuration/upgrade-check'

next:
  text: 'Clone'
  link: '/cmdline/clone'
---

# Command Line Interface (CLI)

Terramate comes with a rich command-line interface, supporting verbosity
levels, logging levels, multiple sub-commands (+experimental), autocompletion
and more.

To view a list of available commands and global flags, execute `terramate --help`.
All sub-commands support the `--help` flag as well for specific details.

## Options

- `-h, --help`                         Show context-sensitive help..
- `-C, --chdir=STRING`                 Sets working directory.
- `-B, --git-change-base=STRING`       Git base ref for computing changes.
- `-v, --verbose=0`                    Increase verboseness of output.

- `--tags=TAGS`                        Filter stacks by tags. Use ":" for logical AND and "," for logical OR. Example: --tags app:prod filters. Stacks containing tag "app" AND "prod". If multiple --tags are provided, an OR expression is created. Example: "--tags a --tags b" is the same as "--tags a,b".
- `--no-tags=NO-TAGS,...`              Filter stacks that do not have the given tags.

- `--log-level="warn"`                 Log level to use: 'disabled', 'trace', 'debug', 'info', 'warn', 'error', or 'fatal'
- `--log-fmt="console"`                Log format to use: 'console', 'text', or 'json'.
- `--log-destination="stderr"`         Destination of log messages.
- `--quiet`                            Disable output.

<!-- - `--disable-check-git-untracked`      Disable git check for untracked files. -->
<!-- - `--disable-check-git-uncommitted`    Disable git check for uncommitted files. -->
<!-- - `--disable-checkpoint`               Disable checkpoint checks for updates. -->
<!-- - `--disable-checkpoint-signature`     Disable checkpoint signature. -->

## Auto Completions

Terramate supports autocompletion of commands for `bash`, `zsh` and `fish`. To
install the completion just run the following command:

```bash
terramate install-completions
```

# CLI Configuration File

Terramate supports a per-user configuration file called `.terramaterc` (or
`terramate.rc` on Windows) which applies to all Terramate projects in the user's
machine by setting up default values for some CLI flags.

The configuration file is a simple HCL file containing top-level attributes.
The attribute expressions must only contain literal values (`number`, `string`,
etc) and no function calls.

Not all CLI flags can be configured by the configuration file.

Below is a list of options:

- `user_terramate_dir` (`string`)

Configures an alternative location for the local `~/.terramate.d` (or `%APPDATA%/.terramate.d`
on Windows).

- `disable_checkpoint` (`boolean`)

When set to `true`, disables [upgrade and security bulletin checks](../configuration/upgrade-check.md). This is similar to exporting the `DISABLE_CHECKPOINT=1` environment variable.

- `disable_checkpoint_signature` (`boolean`)

 when set to `true`, still allows the [upgrade and security bulletin checks](../configuration/upgrade-check.md)
 described above but disables the use of an anonymous id used to de-duplicate warning messages.

## Location

The configuration should be placed in a different path depending on the operating
system:

On _Windows_, the file must be named `terraform.rc` and placed in the user's
`%APPDATA%` directory. The location of this directory depends on your _Windows_
version and system configuration. You can use the command below in _PowerShell_ to
find its location:

```PowerShell
$env:APPDATA
```

On Unix-based systems (_Linux_, _MacOS_, _*BSD_, etc), the file must be named
`.terraformrc` and placed in the home directory of the relevant user.

The default location of the Terramate CLI configuration file can also be specified
using the `TM_CLI_CONFIG_FILE` environment variable.
Example:

```bash
TM_CLI_CONFIG_FILE=/etc/terramaterc terramate run -- <cmd>
```
