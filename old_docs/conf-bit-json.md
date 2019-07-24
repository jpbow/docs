---
id: conf-bit-json
title: Options
permalink: docs/conf-bit-json.html
layout: docs
category: Configuring Bit
next: conf-config.html
prev: conf-files.html
---

This document specifies all the different configurations that are set in `bit` configuration.

## Overview

First of all, let's take a look at the file:

```json
{
    "env": {
        "compiler": "bit.envs/compilers/react@0.0.3",
        "tester": "bit.envs/testers/karma-mocha-react@0.0.18"
    },
    "saveDependenciesAsComponents": "true",
    "packageManager": "yarn",
    "packageManagerArgs": ["--production", "--no-optional"],
    "packageManagerProcessOptions": {
        "shell": true
    },
    "useWorkspaces": "",
    "manageWorkspaces": "true",
    "componentsDefaultDirectory": "components/{name}",
    "dependenciesDirectory": "components/.dependencies",
    "dist": {
        "entry": "src",
        "target": "dist"
    },
    "extensions": {
        "ext-docs-parser": {
            "config": {},
            "options": {
                "core": true
            }
        }
    },
    "resolveModules": {
        "modulesDirectories": ["src"],
        "aliases": {
            "@": "someDir"
        }
    },
    "overrides": {
        "ui/*": {
            "peerDependencies": {
                "react-dom": "+"
            },
            "env": {
                "compiler": "react@16.0.0"
            }
        }
    }
}
```

## Configurations

### `env`

Type: `object`

```json
"env": {
        "compiler": "bit.envs/compilers/react@0.0.3",
        "tester": "none"
    },
```

The `env` section configures your [compiler](/docs/ext-compiling.html) and [tester](/docs/ext-testing.html) [environments](/docs/ext-concepts.html#extensions-vs-environments). If you have a compiler/tester configured, it's full component id and version will be listed here. When no tester/compiler is configured, value will be `none`.
Compilers and testers are not configured manually, but rather by [importing](/docs/cli-import.html#import-a-new-environment) them.

### `saveDependenciesAsComponents`

Type: `boolean`
Default `false`

Imported component dependencies are installed as modules using a package manager or imported with
Bit.

### `packageManager`

Type: `"npm" | "yarn"`
Default: `npm`

Which package manager Bit uses when installing component's package dependencies.

### `componentsDefaultDirectory`

Type: `string`
Default: `"components/{name}`

Default directory for imported components. Relative to the workspace configuration location.

### `dependenciesDirectory`

Type: `string`
Default: `"components/.dependencies"`

Location for imported component dependencies of components.

* Relevant when `saveDependenciesAsComponents:true`

### `dist`

Type: `{ "entry": "src", "target": "dist" }`

* `dist` - target directory for component build artifacts. Default target is component's directory.
* `entry` - The entry point for the dist files (e.g. if your component has an ‘src’ directory that contains all the files, you should set is as the entry point).

### `resolveModules`

Configure custom module resolution for Bit components. This is similar to Webpack’s resolve, and contains 2 objects:

* `moduleDirectories: []` - Add additional paths to resolve components from.
* `aliases` - Sets an alias for a directory.

```js
"resolveModules": {
  "modulesDirectories": ["src"],
  "aliases": {
    "@": "someDir"
  }
}
```

### `useWorkspaces`

Type: `boolean`
Default: `false`

Set whether to use [yarn workspaces](https://yarnpkg.com/blog/2017/08/02/introducing-workspaces/).

* Only relevant when package manager is `yarn`.

### `manageWorkspaces`

Type: `boolean`
Default: `false`

Bit automatically configures each imported component directory in the root `package.json`, in the `workspaces` section.

* Only relevant when `useWorkspaces:true` and `packageManager:"yarn"`.
* Bit manages `componentsDefaultDirectory` and `dependenciesDirectory` and all [custom import
  paths](https://docs.bit.dev/docs/cli-import.html#import-a-single-component-from-a-remote-collection).
* Bit marks root `package.json` as `private:true`.

### `packageManagerArgs`

Type: `string[]`

Specify npm or yarn install arguments.

### `packageManagerProcessOptions`

Type: `object`

configures additional options for the child-process running the package manager.
The available options are the following execa options: `shell`, `env`, `extendEnv`, `uid`, `gid`, `preferLocal`, `localDir`, `timeout`.

### overrides

Type: `object`

This option, allows manual modification to specific, or group of, components. A few usage examples are:

* Removing/adding dependencies.
* Setting different compiler for components.
* Modify dependency version.

Read more [here](/docs/component-dependencies.html#override-dependencies-in-workspace-configuration)
