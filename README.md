Overview
========

This module contains a few usefull functions for operating paths, PATH variable and PowerShell modules paths.

Installation
============

Install from [PowershellGallery](http://www.powershellgallery.com/packages/PathUtils):

```console
> Install-Module -Name PathUtils
```

Usage
=====

### Add some path to PATH variable:

```console
> "c:\Program Files\Java\jdk1.8.0_74\bin\" | Add-ToPath
> java
Usage: java [-options] class [args...]
     (to execute a class)
```
> Note: By default, the variable is modified in the process scope. If you want to persist the change, add `-p` switch


### Refresh PATH variable (i.e. when modified by some other process)

```console
> Refresh-Env
```

### Check if given command is available on PATH (like where/which)

```console
> Where-Is notepad

Source                               Name        CommandType Version
------                               ----        ----------- -------
c:\Program Files\Git\usr\bin\notepad notepad     Application
c:\Windows\System32\notepad.exe      notepad.exe Application
C:\Windows\notepad.exe               notepad.exe Application
```

### Use a PowerShell module directly from source control
Let's say you found a usefull PowerShell module, like this one and you want to hack a little on it. Instead of dropping it in your `PsModulesPath`, you could use `mklink` to add a link to it in some predefined modules location.

```console
> git clone https://github.com/qbikez/ps-pathutils
> Install-ModuleLink ps-pathutils/src/pathutils
```

> Note: this command calls `mklink` underneath to creata a link in global modules directory (`c:\Program Files\WindowsPowerShell\Modules') and requires elevation.

While you're onto that, you can pull latest changes for this linked module, using `Update-ModuleLink`:

```console
> update-modulelink pathutils
running git pull in 'C:\src\ps-modules\pathutils\src\pathutils'
Already up-to-date.
```
