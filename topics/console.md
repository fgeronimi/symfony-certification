---
title: Console - Symfony Certification Preparation List
---
[Back to index](../readme.md#table-of-contents)

# Console
- [The Console Component - symfony.com](https://symfony.com/doc/5.0/components/console.html)

Defining the $defaultDescription static property instead of using the setDescription() method allows to get the command description without instantiating its class. This makes the php bin/console list command run much faster.

If you want to always run the list command fast, add the --short option to it (php bin/console list --short). This will avoid instantiating command classes, but it won't show any description for commands that use the setDescription() method instead of the static property.

The configure() method is called automatically at the end of the command constructor.

Sections are created with the ConsoleOutput::section() method, which returns an instance of ConsoleSectionOutput

Commands have three lifecycle methods that are invoked when running the command:

initialize() (optional)
This method is executed before the interact() and the execute() methods. Its main purpose is to initialize variables used in the rest of the command methods.
interact() (optional)
This method is executed after initialize() and before execute(). Its purpose is to check if some of the options/arguments are missing and interactively ask the user for those values. This is the last place where you can ask for missing options/arguments. After this command, missing options/arguments will result in an error.
execute() (required)
This method is executed after interact() and initialize(). It contains the logic you want the command to execute and it must return an integer which will be used as the command exit status.

## Built-in commands
- [Using Console Commands, Shortcuts and Built-in Commands - symfony.com](https://symfony.com/doc/5.0/components/console/usage.html)

## Custom commands
- [Console Commands - symfony.com](https://symfony.com/doc/5.0/console.html)

## Configuration
- [Configuring the Command - symfony.com](https://symfony.com/doc/5.0/console.html#configuring-the-command)

## Options and arguments
- [Console Input (Arguments & Options)](https://symfony.com/doc/5.0/console/input.html)

## Input and Output objects

## Built-in helpers
- [The Console Helpers - symfony.com](https://symfony.com/doc/5.0/components/console/helpers/index.html)

## Console events
- [Using Events - symfony.com](https://symfony.com/doc/5.0/components/console/events.html)

## Verbosity levels
- [Verbosity levels](https://symfony.com/doc/5.0/console/verbosity.html)
The verbosity level can also be controlled globally for all commands with the SHELL_VERBOSITY environment variable (the -q and -v options still have more precedence over the value of SHELL_VERBOSITY):
