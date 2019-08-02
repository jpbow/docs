---
id: cli
title: CLI Commands
sidebar_label: CLI Commands
---


Bit cli commands

Commands that are marked as workspace only must be executed inside a workspace. Commands that are marked as not workspace only, can be executed from anywhere and will run on a remote server.

---

## add

alias: `a`

Workspace only: yes

`bit add <files | directory | pattern >`
Tracks any set of files as a single or multiple components. Specify a set of files, or a glob pattern of all the files to be added. Check [tracking components](//todo).

**Track a single file as component**: 

```bash
bit add src/foo/bar.js
```

**Track multiple components**:

```bash
bit add src/foo/bar.js src/utils/connect.js
```

**Track a whole directory as a single component**:

```bash
bit add src/foo/
```

**Track each sub directory as a component**:

```bash
bit add src/**/
```

| **Option** | **Alias** | **Description**
|---|---|---|
|`--id <id>` | `-i` | Component's ID of the files added 
|`--main <file>` | `-m` | The component entry point
|`--tests <tests>` | `-t-` | Specify a test file, test files directory, or tests path
|`--namespace <namespace>` | `-n` | Add multiple components to the same namespace 
|`--exclude <file...>` | `-e` | exclude files, directory or patterns 
|`--override <true>`  | `-o` | override existing components. default = false 

---

## build

Workspace only: yes

`bit build [id]`

Build the component with the default or specified compiler. Default compiler is defined in the bit configuration(//todo). 
Build command is automatically performed before a component is tagged. Building a component may change the component if its dependencies were changed.

**Build all components**:

```bash
bit build
```

**Build a single component**:

```bash
bit build foo/bar
```

| **Option** | **Alias** | **Description**
|---|---|---|
|`--verbose` | `-v` | Show verbose output 
|`--no-cache` | `-c` | Ignore component build files cache

---

## checkout

alias: `c`
Workspace only: yes

Merge the version of the sourced component(s) to your workspace

`bit checkout <version|latest> <component id...>`

Replace the working files of the component(s) with the specified version's incoming files. This will perform a `git merge` on the files, unless reset was requested.

Checkout a single component:

```bash
bit checkout 0.0.3 foo/bar
```

Checkout multiple components to latest version: 

```bash
bit checkout latest foo/bar sun/moon
```

Checkout all incoming components to the version: 

```bash
bit checkout 0.0.3 --all
```

| **Option** | **Alias** | **Description**
|---|---|---|
|`--interactive-merge` | `-i` | Display options to resolve conflicts with merged files of the components 
|`--ours` | `-o` | Override conflicting files with the current version's files
|`--theirs` | `-t` | Override conflicting files with the version's files
|`--manual` | `-m` | leave the files in conflicted stage for later resolution
|`--reset` | `-r` | Remove local changes and apply version's changes
|`--all` | `-a` | Checkout all imported components
|`--verbose` | `-v` | Show verbose output
|`--skip-npm-install` | | Do not install npm packages for imported components. 
|`--ignore dist` |  | Do not write dist files for incoming components

---

## deprecate

alias: `d`

Workspace only: no

`bit deprecate <Ids...>`

Marks a local or a remote component as deprecated

Mark local component as deprecated:

```bash
bit deprecate foo/bar
```

Mark remote component as deprecated:

```bash
bit deprecate me.collection/foo/bar --remote
```

| **Option** | **Alias** | **Description**
|---|---|---|
|`--remote` | `-r` | deprecate a component from a remote collection

---

## diff

Workspace only: yes

`bit diff <Ids...> [version version]`

Show differences between components' files locally. Rum `bit import` to get versions from the remote collection. 

Compare all the component in working directory to their latest version in local workspace:

```bash
bit diff
```

Compare a single component in working directory to local scope:

```bash
bit diff me.collection/foo/bar
```

Compare the component in working directory to the specified version in local workspace:

```bash
bit diff me.collection/foo/bar 1.0.0
```

Compare between two specific versions of a component in local workspace:

```bash
bit diff me.collection/foo/bar 1.0.0 2.0.0
```

| **Option** | **Alias** | **Description**
|---|---|---|
|`--verbose` | `-v` | Show detailed output

---

## doctor

Workspace only: yes

`bit doctor`

Run diagnosis on your workspace, to view errors and fixing hints. Send output to maintainers for help with errors resolution. 

| **Option** | **Alias** | **Description**
|---|---|---|
|`--save <filename>` | `-s` | save output to filename
|`--json` | `-j` | Return diagnoses in json format
|`--list` | | List all available diagnoses

---

## eject

Workspace only: yes

`bit eject <component Id ...>`
replaces the components from the local scope with the corresponding NPM packages. If code was modified locally, use `--force` to override.

| **Option** | **Alias** | **Description**
|---|---|---|
|`--force` | `-f` | Ignore local version. Eject the components even when they are staged or modified
|`--json` | `-j` | Print the results in JSON format

---

## export

`bit export <remote> [id...]`
Push staged component(s) to a remote Collection.

**Export all staged components to the same Collection**: 

```bash
bit export me.collection
```

**Export a specific component to a Collection**:

```bash
bit export me.collection foo/bar
```

| **Option** | **Alias** | **Description**
|---|---|---|
|`--eject` | `-e` | Replaces the exported components from the local scope with the corresponding packages.

---

## import

alias: `i`

`bit import [id...|pattern][@version]`

Import components into current workspace. Can specify specific component(s) and their versions. The component will be imported to the default location specified in the [configuration](workspace/#componentsdefaultdirectory)

| **Option** | **Alias** | **Description**
|---|---|---|
|`--tester` | `-t` | Import a tester component 
|`--compiler` | `-c` | Import a compiler component
|`--extension`  | `-x` | Import an extension component
|`--environment` | `-e` | Install component's compiler and tester during import.



|  -p|  --path <path> | Import components into a specific directory
|  -o|  --objects           | import components objects only, don't write the components to the file system. This is a default behavior for import with no id
|  -d|  --display-dependencies | display the imported dependencies
|  -O|  --override          | override local changes
|  -v|  --verbose           | showing verbose output for inspection
|    | --ignore-dist           | write dist files (when exist) to the configured directory
|    |--conf [path]           | write the configuration file (bit.json) and the envs configuration files (use --conf without path to write to the default dir)
|    |  --| skip-npm-install      | do not install packages of the imported components. (it automatically enables |save| dependencies-as-components flag)
|    |--ignore-package-json   | do not generate package.json for the imported component(s). (it automatically enables skip-npm-install |and have-dependencies-as-components flags)
|  -m| --merge [strategy]  | merge local changes with the imported version. strategy should be "theirs", "ours" or "manual"
