# Write The First App

**Gini** is a __module-based framework__. Every Gini App is just a module in gini module directory, `$HOME/gini-modules` locally or `/usr/local/share/gini-modules` globally depends on your configuration (see [Installation](get-started/install.html)). Be sure to configure your shell environment before start.

### Create an App
```bash
$ cd $HOME/gini-modules
$ mkdir sample
$ cd sample
$ gini init
Shortname [sample]:
Name [Sample]:
Description [App description...]:
Version [0.1]:
Dependencies [N/A]:
$ _
```
It will generate `gini.json` in app directory according your input.
```json
{
    "id": "sample",
    "name": "Sample",
    "description": "App description...",
    "version": "0.1",
    "dependencies": ""
}
```
